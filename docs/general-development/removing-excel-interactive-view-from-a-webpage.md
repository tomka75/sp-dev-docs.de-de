---
title: Entfernen einer interaktiven Excel-Ansicht von einer Webseite
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 407b3aa3-7286-462b-905f-811a3b7f3f1c
ms.openlocfilehash: d91eefbcbb34967acca01da89d60a914d681a46b
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
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
  
    
    

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Excel Services in SharePoint](excel-services-in-sharepoint.md)
    
  
-  [Einbetten einer Excel-Arbeitsmappe in Ihren Blog](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU)
    
  

