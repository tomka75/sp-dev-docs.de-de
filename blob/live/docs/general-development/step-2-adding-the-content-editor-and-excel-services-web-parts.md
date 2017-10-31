---
title: Step 2 Adding the Content Editor and Excel Services Web Parts
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c9c66843-fd77-4a0d-a512-d936d15d4429
ms.openlocfilehash: cad2e53b4a7284fc0a5de7205635e26b01c0bcd3
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="step-2-adding-the-content-editor-and-excel-services-web-parts"></a><span data-ttu-id="d65e9-102">Step 2: Adding the Content Editor and Excel Services Web Parts</span><span class="sxs-lookup"><span data-stu-id="d65e9-102">Step 2: Adding the Content Editor and Excel Services Web Parts</span></span>

<span data-ttu-id="d65e9-103">Nachdem Sie eine ECMAScript (JavaScript, JScript)-Textdatei erstellt und an einem vertrauenswürdigen Speicherort gespeichert haben, erstellen Sie im nächsten Schritt eine Webparts-Seite und fügen der Seite das Inhalts-Editor-Webpart und das Excel Services-Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="d65e9-103">After you create an ECMAScript (JavaScript, JScript) text file and save the text file in a trusted location, the next step is to create a Web Parts Page and add the Content Editor Web Part and the Excel Services Web Part to the page.</span></span> 
  
    
    

<span data-ttu-id="d65e9-104">Zeigen Sie als nächstes eine Arbeitsmappe mithilfe des Excel Services-Webparts an, das Sie der Seite hinzugefügt haben.</span><span class="sxs-lookup"><span data-stu-id="d65e9-104">Next, display a workbook by using the Excel Services Web Part that you added to the page.</span></span> 
### <a name="to-add-the-content-editor-web-part-and-the-excel-services-web-part"></a><span data-ttu-id="d65e9-105">So fügen Sie das Inhalts-Editor-Webpart und das Excel Services-Webpart hinzu</span><span class="sxs-lookup"><span data-stu-id="d65e9-105">To add the Content Editor Web Part and the Excel Services Web Part</span></span>


1. <span data-ttu-id="d65e9-106">Erstellen Sie eine neue Webparts-Seite.</span><span class="sxs-lookup"><span data-stu-id="d65e9-106">Create a new Web Parts Page.</span></span> 
    
  
2. <span data-ttu-id="d65e9-107">Fügen Sie der soeben erstellten Webparts-Seite ein Inhalts-Editor-Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="d65e9-107">Add a Content Editor Web Part to the Web Parts Page that you just created.</span></span>
    
  
3. <span data-ttu-id="d65e9-p101">Fügen Sie die URL der Textdatei, die Sie in  [Step 1: Creating a ECMAScript Text File](step-1-creating-a-ecmascript-text-file.md) erstellt haben, dem Inhalts-Editor-Webpart hinzu. Fügen Sie dazu die URL für die Textdatei hinzu, die Sie in [Step 1: Creating a ECMAScript Text File](step-1-creating-a-ecmascript-text-file.md) in eine vertrauenswürdige Dokumentbibliothek hochgeladen haben.</span><span class="sxs-lookup"><span data-stu-id="d65e9-p101">Feed the URL for the text file that you created in  [Step 1: Creating a ECMAScript Text File](step-1-creating-a-ecmascript-text-file.md) to the Content Editor Web Part. You do this by adding the URL for the text file that you uploaded to a trusted document library in [Step 1: Creating a ECMAScript Text File](step-1-creating-a-ecmascript-text-file.md).</span></span> 
    
    <span data-ttu-id="d65e9-110">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d65e9-110">For example:</span></span> 
    
     <span data-ttu-id="d65e9-111">`http://` _meinserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`</span><span class="sxs-lookup"><span data-stu-id="d65e9-111">`http://` _myserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`</span></span>
    
  
4. <span data-ttu-id="d65e9-112">Fügen Sie der Seite ein Excel Services-Webpart hinzu.</span><span class="sxs-lookup"><span data-stu-id="d65e9-112">Add an Excel Services Web Part to the page.</span></span>
    
  

### <a name="to-run-the-ecmascript-sample"></a><span data-ttu-id="d65e9-113">So führen Sie das ECMAScript-Beispiel aus</span><span class="sxs-lookup"><span data-stu-id="d65e9-113">To run the ECMAScript sample</span></span>


1. <span data-ttu-id="d65e9-p102">Laden Sie eine Arbeitsmappe in eine vertrauenswürdige Dokumentbibliothek hoch. Zeigen Sie mithilfe des Menüs **Freigegebenes Webpart bearbeiten** den Aufgabenbereich des Excel Services-Webparts an. Geben Sie im Abschnitt **Arbeitsmappenanzeige** im Feld **Arbeitsmappe** die URL der Arbeitsmappe ein, die vom Excel Services-Webpart geladen und angezeigt werden soll. Beispiel:</span><span class="sxs-lookup"><span data-stu-id="d65e9-p102">Upload a workbook to a trusted document library. Use the **Modify Shared Web Part** menu to display the Excel Services Web Part task pane. In the **Workbook Display** section, in the **Workbook** field, type the URL to the workbook that you want the Excel Services Web Part to load and display. For example:</span></span>
    
     <span data-ttu-id="d65e9-118">`http://` _meinserver_ `/Docs/Documents/WorkbookToDisplay.xlsx`</span><span class="sxs-lookup"><span data-stu-id="d65e9-118">`http://` _myserver_ `/Docs/Documents/WorkbookToDisplay.xlsx`</span></span>
    
  
2. <span data-ttu-id="d65e9-119">Klicken Sie auf verschiedene Zellen, und beobachten Sie, wie der Wert der Zelle im Inhalts-Editor **div** aufgefüllt wird.</span><span class="sxs-lookup"><span data-stu-id="d65e9-119">Try clicking different cells and observe the cell value populated in the Content Editor **div**.</span></span> 
    
  

