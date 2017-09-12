---
title: Step 2 Adding the Content Editor and Excel Services Web Parts
ms.prod: OFFICE365
ms.assetid: c9c66843-fd77-4a0d-a512-d936d15d4429
ms.openlocfilehash: 7ac9f535ad153693214a84ace404f26a631dbac5
ms.sourcegitcommit: d9e955bf9d5afd9ad8ae8304a3ddb85ac27b3406
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2017
---
# <a name="step-2-adding-the-content-editor-and-excel-services-web-parts"></a>Step 2: Adding the Content Editor and Excel Services Web Parts

Nachdem Sie eine ECMAScript (JavaScript, JScript)-Textdatei erstellt und an einem vertrauenswürdigen Speicherort gespeichert haben, erstellen Sie im nächsten Schritt eine Webparts-Seite und fügen der Seite das Inhalts-Editor-Webpart und das Excel Services-Webpart hinzu. 
  
    
    

Zeigen Sie als nächstes eine Arbeitsmappe mithilfe des Excel Services-Webparts an, das Sie der Seite hinzugefügt haben. 
### <a name="to-add-the-content-editor-web-part-and-the-excel-services-web-part"></a>So fügen Sie das Inhalts-Editor-Webpart und das Excel Services-Webpart hinzu


1. Erstellen Sie eine neue Webparts-Seite. 
    
  
2. Fügen Sie der soeben erstellten Webparts-Seite ein Inhalts-Editor-Webpart hinzu.
    
  
3. Fügen Sie die URL der Textdatei, die Sie in  [Step 1: Creating a ECMAScript Text File](step-1-creating-a-ecmascript-text-file) erstellt haben, dem Inhalts-Editor-Webpart hinzu. Fügen Sie dazu die URL für die Textdatei hinzu, die Sie in [Step 1: Creating a ECMAScript Text File](step-1-creating-a-ecmascript-text-file) in eine vertrauenswürdige Dokumentbibliothek hochgeladen haben. 
    
    Beispiel: 
    
     `http://` _meinserver_ `/Docs/Documents/JSOM_FeedToContentEditor.txt`
    
  
4. Fügen Sie der Seite ein Excel Services-Webpart hinzu.
    
  

### <a name="to-run-the-ecmascript-sample"></a>So führen Sie das ECMAScript-Beispiel aus


1. Laden Sie eine Arbeitsmappe in eine vertrauenswürdige Dokumentbibliothek hoch. Zeigen Sie mithilfe des Menüs **Freigegebenes Webpart bearbeiten** den Aufgabenbereich des Excel Services-Webparts an. Geben Sie im Abschnitt **Arbeitsmappenanzeige** im Feld **Arbeitsmappe** die URL der Arbeitsmappe ein, die vom Excel Services-Webpart geladen und angezeigt werden soll. Beispiel:
    
     `http://` _meinserver_ `/Docs/Documents/WorkbookToDisplay.xlsx`
    
  
2. Klicken Sie auf verschiedene Zellen, und beobachten Sie, wie der Wert der Zelle im Inhalts-Editor **div** aufgefüllt wird. 
    
  

