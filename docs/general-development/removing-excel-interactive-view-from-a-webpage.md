---
title: Entfernen einer interaktiven Excel-Ansicht von einer Webseite
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 407b3aa3-7286-462b-905f-811a3b7f3f1c
ms.openlocfilehash: bb8372a12f8f33fcfca26c1917ac6e1800d1c80e
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="removing-excel-interactive-view-from-a-webpage"></a>Entfernen einer interaktiven Excel-Ansicht von einer Webseite

Das Feature „Interaktive Excel-Ansicht“ wurde deaktiviert. Wenn Sie eine interaktive Excel-Ansicht in Ihre Webseite eingefügt haben, können Sie diese entfernen, indem Sie den `<script>`-Tag und die Platzhalter-`<a>`-Tags für die Schaltfläche aus dem HTML-Code Ihrer Webseite entfernen.
  
    
    

Zum Entfernen des `<script>`-Tags suchen und löschen Sie den folgenden HTML-Code.


```HTML

<script src="http://r.office.microsoft.com/r/rlidExcelButton?v=1&amp;amp;kip=1" type="text/javascript"></script>
```

Zum Entfernen der Platzhalter-`<a>`-Tags suchen Sie die <a>-Tags, die sich direkt vor <table> Elementen in Ihrem HTML-Code befinden. Da <a>-Tags anpassbar sind, analysieren Sie den HTML-Code für den ersten Teil der Zeichenfolge, um alle Instanzen der Schaltfläche zu finden.


```HTML
<a href="#" name="MicrosoftExcelButton" data-xl-tableTitle="" data-xl-buttonStyle="Standard" data-xl-fileName="Book1" data-xl-attribution="" ></a>
```


## <a name="workarounds"></a>Problemumgehungen

Alternativ empfehlen wir, [Excel in die Webseiten einzubetten ](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU).
  
    
    

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>


-  [Excel Services in SharePoint](excel-services-in-sharepoint.md)
    
  
-  [Einbetten einer Excel-Arbeitsmappe in Ihren Blog](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU)
    
  

