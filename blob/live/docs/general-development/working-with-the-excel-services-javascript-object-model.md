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
# <a name="working-with-the-excel-services-javascript-object-model"></a><span data-ttu-id="bf10e-102">Arbeiten mit dem Excel Services-JavaScript-Objektmodell</span><span class="sxs-lookup"><span data-stu-id="bf10e-102">Working with the Excel Services JavaScript object model</span></span>

<span data-ttu-id="bf10e-103">Wenn Sie Code mit dem JavaScript-Objektmodell (JSOM) schreiben, gibt es zwei Szenarien, in denen der Code ausgeführt werden kann: Auf einer SharePoint-Seite oder auf einer Host-Webseite mit einer eingebetteten Arbeitsmappe, die auf Microsoft OneDrive gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="bf10e-103">When you write code that uses the JavaScript object model (JSOM), there are two scenarios where the code can run: on a SharePoint page; or on a host webpage that contains an embedded workbook that is stored on Microsoft OneDrive.</span></span> <span data-ttu-id="bf10e-104">Dieser Artikel erläutert die Hauptunterschiede zwischen den beiden Szenarien, die sich erheblich auf das Schreiben des Codes auswirken.</span><span class="sxs-lookup"><span data-stu-id="bf10e-104">This article discusses the main difference between the two scenarios that significantly affect how you write your code.</span></span>
  
    
    


## <a name="using-the-excel-services-jsom"></a><span data-ttu-id="bf10e-105">Verwenden des Excel Services-JSOM</span><span class="sxs-lookup"><span data-stu-id="bf10e-105">Using the Excel Services JavaScript API</span></span>

<span data-ttu-id="bf10e-106">In Tabelle 1 sind die Unterschiede zwischen den beiden Szenarien aufgeführt, die verfügbar sind, wenn Sie Code mit dem JSOM schreiben.</span><span class="sxs-lookup"><span data-stu-id="bf10e-106">Table 1 lists the difference between the two scenarios available when you write code that uses the JSOM.</span></span>
  
    
    

<span data-ttu-id="bf10e-107">**Tabelle 1. Szenarien für Excel Services JSOM**</span><span class="sxs-lookup"><span data-stu-id="bf10e-107">**Table 1. Scenarios for Excel Services JSOM**</span></span>


|<span data-ttu-id="bf10e-108">**Ort**</span><span class="sxs-lookup"><span data-stu-id="bf10e-108">**Location**</span></span>|<span data-ttu-id="bf10e-109">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="bf10e-109">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="bf10e-110">**OneDrive**</span><span class="sxs-lookup"><span data-stu-id="bf10e-110">**OneDrive**</span></span> <br/> |<span data-ttu-id="bf10e-111">In diesem Szenario betten Sie eine Arbeitsmappe, die auf OneDrive gespeichert ist, in die Host-Webseite mit einem HTML-Element</span><span class="sxs-lookup"><span data-stu-id="bf10e-111">In this scenario, you embed a workbook that is stored on OneDrive into the host webpage using an HTML</span></span> <div> <span data-ttu-id="bf10e-112">ein.</span><span class="sxs-lookup"><span data-stu-id="bf10e-112">Element</span></span> <span data-ttu-id="bf10e-113">Dann fügen Sie Code in die Seite ein, die mit der eingebetteten Arbeitsmappe interagiert.</span><span class="sxs-lookup"><span data-stu-id="bf10e-113">Then you include code in the page that interacts with the embedded workbook.</span></span>  <br/> |
|<span data-ttu-id="bf10e-114">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="bf10e-114">**SharePoint**</span></span> <br/> |<span data-ttu-id="bf10e-115">In diesem Szenario wird eine SharePoint-Seite von SharePoint bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="bf10e-115">In this scenario, you have a SharePoint page served by SharePoint.</span></span> <span data-ttu-id="bf10e-116">Sie fügen ein Webpart in die SharePoint-Seite ein, das eine an einem vertrauenswürdigen Speicherort gespeicherte Arbeitsmappe enthält.</span><span class="sxs-lookup"><span data-stu-id="bf10e-116">You insert an Web Part into the SharePoint page that contains a workbook that is stored in an trusted location.</span></span> <span data-ttu-id="bf10e-117">Dann fügen Sie Code in die SharePoint-Seite ein, die mit dem Webpart interagiert.</span><span class="sxs-lookup"><span data-stu-id="bf10e-117">Then you include code in the SharePoint page that interacts with the Web Part.</span></span>  <br/> |
   
<span data-ttu-id="bf10e-118">Der Hauptunterschied beim Schreiben von Code für die beiden Szenarien liegt im Abrufen des Verweises zum Objekt [Ewa.EwaControl](http://msdn.microsoft.com/library/6e441406-d67a-0da9-f996-71f4e4b4c144%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf10e-118">The main difference between writing code for the two scenarios is how you get a reference to the  [Ewa.EwaControl](http://msdn.microsoft.com/library/6e441406-d67a-0da9-f996-71f4e4b4c144%28Office.15%29.aspx) object.</span></span> <span data-ttu-id="bf10e-119">Da **[Ewa.EwaControl]** der Einstiegspunkt zum JavaScript-Objektmodell ist, müssen Sie einen Verweis für die Zusammenarbeit mit dem JSOM herstellen.</span><span class="sxs-lookup"><span data-stu-id="bf10e-119">Because the **[Ewa.EwaControl]** is the entry point to the JavaScript object model, you must get a reference to it to work with the JSOM.</span></span>
  
    
    

### <a name="getting-a-reference-to-the-ewacontrol-object-sharepoint"></a><span data-ttu-id="bf10e-120">Abrufen eines Verweises auf das Objekt EwaControl (SharePoint)</span><span class="sxs-lookup"><span data-stu-id="bf10e-120">Getting a reference to the EwaControl object (SharePoint)</span></span>

<span data-ttu-id="bf10e-121">Wenn Sie Code schreiben, der mit einem Webpart auf einer SharePoint-Seite interagiert, erhalten Sie einen Verweis auf das Objekt **[Ewa.EwaControl]**, indem Sie die Methode [Ewa.EwaControlCollection.getItem(index)](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx) wie im folgenden Codebeispiel gezeigt verwenden.</span><span class="sxs-lookup"><span data-stu-id="bf10e-121">When writing code that interacts with an Web Part on a SharePoint page, you get a reference to the **[Ewa.EwaControl]** object by using the method, [Ewa.EwaControlCollection.getItem(index)](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx), as shown in the following code example.</span></span>
  
    
    

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


### <a name="getting-a-reference-to-the-ewacontrol-object-onedrive"></a><span data-ttu-id="bf10e-122">Abrufen eines Verweises auf das Objekt EwaControl (OneDrive)</span><span class="sxs-lookup"><span data-stu-id="bf10e-122">Getting a reference to the EwaControl object (OneDrive)</span></span>

<span data-ttu-id="bf10e-123">Wenn Sie Code schreiben, der mit einer eingebetteten Arbeitsmappe interagiert, die auf OneDrive gespeichert ist, erhalten Sie einen Verweis auf das Objekt **[Ewa.EwaControl]** mithilfe des Objekts [AsyncResult](http://msdn.microsoft.com/library/1da51396-834c-d85b-a9b0-ce21e4329946%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf10e-123">When writing code that interacts with an embedded workbook that is stored on OneDrive, you get a reference to the **[Ewa.EwaControl]** object through the [AsyncResult](http://msdn.microsoft.com/library/1da51396-834c-d85b-a9b0-ce21e4329946%28Office.15%29.aspx) object.</span></span> <span data-ttu-id="bf10e-124">Das Objekt **[AsyncResult]** wird in einem einzigen Parameter an die Rückrufmethode übergeben, die Sie in der statischen Methode [Ewa.EwaControl.loadEwaAsync](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx) angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="bf10e-124">The **[AsyncResult]** object is passed in as the single parameter to the callback method that you specify in the [Ewa.EwaControl.loadEwaAsync](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx) static method.</span></span> <span data-ttu-id="bf10e-125">Wenn der Rückruf aufgerufen wird, ist ein Verweis auf das Objekt **[Ewa.EwaControl]** im Objekt **[AsyncResult]** enthalten.</span><span class="sxs-lookup"><span data-stu-id="bf10e-125">When the callback is invoked, a reference to the **[Ewa.EwaControl]** object is included in the **[AsyncResult]** object.</span></span> <span data-ttu-id="bf10e-126">Das folgende Codebeispiel zeigt, wie Sie einen Verweis auf das Objekt **[Ewa.EwaControl]** über das Objekt **[AsyncResult]** erhalten.</span><span class="sxs-lookup"><span data-stu-id="bf10e-126">The following code example shows how you get a reference to the **[Ewa.EwaControl]** object through the **[AsyncResult]** object.</span></span>
  
    
    

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


### <a name="conclusion"></a><span data-ttu-id="bf10e-127">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="bf10e-127">Conclusion</span></span>

<span data-ttu-id="bf10e-128">Das Schreiben eines Entwurfs mithilfe des JavaScript-Objektmodells ist für SharePoint und eine Host-Webseite im Wesentlichen identisch.</span><span class="sxs-lookup"><span data-stu-id="bf10e-128">Writing a solution that uses the JavaScript object model is basically the same whether the solution runs on SharePoint or on a host webpage.</span></span> <span data-ttu-id="bf10e-129">Der Hauptunterschied besteht im Abrufen des Objekts **[Ewa.EwaControl]**.</span><span class="sxs-lookup"><span data-stu-id="bf10e-129">The main difference is how you get a reference to the **[Ewa.EwaControl]** object.</span></span> <span data-ttu-id="bf10e-130">Wenn Sie über einen Verweis zum Objekt **[Ewa.EwaControl]** verfügen, ist der Rest des Codes, den Sie schreiben, für beide Szenarien etwa gleich.</span><span class="sxs-lookup"><span data-stu-id="bf10e-130">Once you have a reference to the **[Ewa.EwaControl]** object, the rest of the code that you write will be almost the same for both scenarios.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="bf10e-131">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="bf10e-131">Additional resources</span></span>
<span data-ttu-id="bf10e-132"><a name="SP15DevKitchenCon_AnatomyofanappSignupsheets_Additionalresources"> </a></span><span class="sxs-lookup"><span data-stu-id="bf10e-132"></span></span>


-  <span data-ttu-id="bf10e-133">
  [Verwenden der Excel Services-JavaScript-API zum Arbeiten mit eingebetteten Excel-Arbeitsmappen](http://msdn.microsoft.com/en-us/library/hh315812.aspx)</span><span class="sxs-lookup"><span data-stu-id="bf10e-133">[Using the Excel Services JavaScript API to Work with Embedded Excel Workbooks](http://msdn.microsoft.com/en-us/library/hh315812.aspx)</span></span>
    
  
-  [<span data-ttu-id="bf10e-134">Ewa.EwaControl.loadEwaAsync</span><span class="sxs-lookup"><span data-stu-id="bf10e-134">Ewa.EwaControl.loadEwaAsync</span></span>](http://msdn.microsoft.com/library/a7ee4d6d-5472-b942-c78e-b368d30bcb0e%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="bf10e-135">Ewa.EwaControlCollection.getItem(index)</span><span class="sxs-lookup"><span data-stu-id="bf10e-135">Ewa.EwaControlCollection.getItem(index)</span></span>](http://msdn.microsoft.com/library/11dd3a65-f914-4b34-bbaf-0206c8153d2b%28Office.15%29.aspx)
    
  

