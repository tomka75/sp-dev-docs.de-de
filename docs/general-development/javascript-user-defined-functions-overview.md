---
title: "Benutzerdefinierte JavaScript-Funktionen (Übersicht)"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: fee38837-1985-4319-ba4e-b99c6ec66336
ms.openlocfilehash: 8c4a4d867fc19d84b05b81497272e39d72f27118
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="javascript-user-defined-functions-overview"></a>Benutzerdefinierte JavaScript-Funktionen (Übersicht)
Benutzerdefinierte JavaScript-Funktionen (UDFs) sind neu in Excel Services und SharePoint. Dieser Artikel bietet eine allgemeine Übersicht über JavaScript UDFs, einschließlich grundlegender Informationen über deren Funktionsweise in Excel Services.
## <a name="what-are-udfs"></a>Was sind UDFs?
<a name="xlsWhatAreUdfs"> </a>

Eine benutzerdefinierte Funktion (UDF) ist eine Funktion, die Sie selbst erstellen können, und fügen Sie der Liste der verfügbaren Funktionen in Excel beim Excel dem Typ der Funktion zur Verfügung steht, sofort einsetzbar werden soll.
  
    
    
Excel Services already allows you to create UDFs using managed code, so if you have worked with the existing Excel Services UDFs, JavaScript UDFs should look familiar to you. For more information about creating UDFs using managed code, see  [Excel Services User-Defined Functions](excel-services-user-defined-functions.md).
  
    
    

## <a name="javascript-udfs"></a>JavaScript-UDFs
<a name="xlsJsUDFs"> </a>

JavaScript-UDFs sind UDFs, die auf einer Webseite im Browser ausgeführt werden, die eine Arbeitsmappe eingebettete Excel hat. Verwenden Sie die JavaScript UDF in die eingebettete Arbeitsmappe. Solange Sie mit der Arbeitsmappe im Browser arbeiten, können Sie die JavaScript UDF genau, wie Sie die integrierte Excel-Funktionen verwenden. Wenn die Webseite geschlossen wird, ist die JavaScript UDF nicht mehr verfügbar.
  
    
    

## <a name="how-do-javascript-udfs-work"></a>Funktionsweise von JavaScript-UDFs
<a name="xlsJsUDFs"> </a>

Um eine JavaScript UDF zu verwenden, müssen Sie haben die Möglichkeit zum Ändern des Inhalts der Webseite, in dem Sie die Arbeitsmappe einbetten. Nachdem Sie die richtigen Excel Services JavaScript-Quelldatei verweisen möchten, fügen Sie Ihrer JavaScript UDF-Code auf der Seite. Darüber hinaus vor der Verwendung von JavaScript UDF müssen Sie zuerst die UDF-Datei mit der Dienste für Excel-Berechnungen zu registrieren. JavaScript UDF-API stellt Methoden zum Registrieren und Aufheben der Registrierung Ihrer JavaScript UDF bereit.
  
    
    
Wenn die Webseite mit den Excel Web Access-Webpart oder eingebetteten Arbeitsmappe gerendert wird, können Sie die JavaScript UDF in der Arbeitsmappe genau wie jede andere Excel Arbeitsmappe aufrufen.
  
    
    
Sie möglicherweise beispielsweise eine Funktion, die den aktuellen Aktienkurs für eine bestimmte Aktie abruft. Sie können die Webseite eine UDF JavaScript hinzufügen, die Ihre Excel-Arbeitsmappe (vorausgesetzt, dass Sie über Schreibrechte für die Webseite verfügen) gehostet wird, die JavaScript Code wie folgt verwendet.
  
    
    



```

function StockInfo(symbol, measure) {
  var req = new XMLHttpRequest();
  req.open('GET', 'http://www.contoso-stock-quotes.com/quote/' + symbol + '/' + measure, false); 
  req.send(null);
  if (req.status == 200) {
    return req.responseText;
  } else {
    throw new Error(ExcelCalcError.Value);
  }
 
ewa.BrowserUdfs.add("StockQuote",
                       StockInfo,
                       "Gets a stock quote given a security symbol and measure to return."
                       false,
                       false
                       );

```

Sie können die JavaScript UDF, StockInfo, klicken Sie dann in einer Formel aus einer Zelle innerhalb der Excel Online aufrufen.
  
    
    

**Abbildung 1. JavaScript UDF, die in Excel Online aufgerufen werden.**

  
    
    

  
    
    
![In Excel Online aufgerufene benutzerdefinierte JavaScript-Funktionen](../images/SPS15CON_xls_JsUdfinWebApp.jpg)
  
    
    

  
    
    

  
    
    

## <a name="where-can-i-use-javascript-udfs"></a>Wo kann ich JavaScript UDFs verwenden?
<a name="xlsWhereUseJsUdfs"> </a>

JavaScript UDFs können entweder in Arbeitsmappen, die in SharePoint Excel Web Access-Webparts angezeigt werden, oder in Arbeitsmappen, die in eine Host-Webseite eingebettet sind, erstellt und verwendet werden. Die Arbeitsmappe muss auf Microsoft OneDrive gespeichert werden. Der Hauptunterschied besteht darin, dass JavaScript-UDFs, die zu Excel Web Access-Webparts hinzugefügt werden, einen SharePoint-Server erfordern. Bei JavaScript-UDFs, die zu Host-Webseiten mit eingebetteten Arbeitsmappen hinzugefügt werden, muss die Arbeitsmappe lediglich auf OneDrive gespeichert werden.
  
    
    

## <a name="key-points"></a>Wichtige Punkte
<a name="xlsWhereUseJsUdfs"> </a>


- JavaScript-UDFs live nur, solange die Webseite, die, der Sie auf, angezeigt wird. Sie nicht über die Lebensdauer der Webseite hinaus erhalten bleiben, in dem sie erstellt wurden.
    
  
- Sie können keine Excel Services JavaScript-Objektmodell aus in einer JavaScript UDF aufrufen.
    
  

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Excel Services in SharePoint](excel-services-in-sharepoint.md)
    
  
-  [Was ist neu in Excel Services für Entwickler](http://msdn.microsoft.com/library/09e96c8b-cb55-4fd1-a797-b50fbf0f9296.aspx)
    
  
-  [Benutzerdefinierte Funktionen von Excel Services](http://msdn.microsoft.com/de-DE/library/ms493934)
    
  

