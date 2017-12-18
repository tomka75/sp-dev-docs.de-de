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
# <a name="removing-excel-interactive-view-from-a-webpage"></a><span data-ttu-id="904e8-102">Entfernen einer interaktiven Excel-Ansicht von einer Webseite</span><span class="sxs-lookup"><span data-stu-id="904e8-102">Removing Excel Interactive View from a webpage</span></span>

<span data-ttu-id="904e8-103">Das Feature „Interaktive Excel-Ansicht“ wurde deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="904e8-103">The Excel Interactive View feature has been disabled.</span></span> <span data-ttu-id="904e8-104">Wenn Sie eine interaktive Excel-Ansicht in Ihre Webseite eingefügt haben, können Sie diese entfernen, indem Sie den `<script>`-Tag und die Platzhalter-`<a>`-Tags für die Schaltfläche aus dem HTML-Code Ihrer Webseite entfernen.</span><span class="sxs-lookup"><span data-stu-id="904e8-104">If you have inserted an Excel Interactive View into your web page, you can remove it by removing the  `<script>` tag and the placeholder `<a>` tags for the button from the HTML of your web page.</span></span>
  
    
    

<span data-ttu-id="904e8-105">Zum Entfernen des `<script>`-Tags suchen und löschen Sie den folgenden HTML-Code.</span><span class="sxs-lookup"><span data-stu-id="904e8-105">To remove the  `<script>` tag, search for and delete the following HTML.</span></span>


```HTML

<script src="http://r.office.microsoft.com/r/rlidExcelButton?v=1&amp;amp;kip=1" type="text/javascript"></script>
```

<span data-ttu-id="904e8-106">Zum Entfernen der Platzhalter-`<a>`-Tags suchen Sie die <a>-Tags, die sich direkt vor</span><span class="sxs-lookup"><span data-stu-id="904e8-106">To remove the placeholder  `<a>` tags, find <a> tags that are located directly before any</span></span> <table> <span data-ttu-id="904e8-107">Elementen in Ihrem HTML-Code befinden.</span><span class="sxs-lookup"><span data-stu-id="904e8-107">elements in your HTML.</span></span> <span data-ttu-id="904e8-108">Da <a>-Tags anpassbar sind, analysieren Sie den HTML-Code für den ersten Teil der Zeichenfolge, um alle Instanzen der Schaltfläche zu finden.</span><span class="sxs-lookup"><span data-stu-id="904e8-108">Because <a> tags are customizable, parse your HTML for the first part of the string to find all the instances of the button.</span></span>


```HTML
<a href="#" name="MicrosoftExcelButton" data-xl-tableTitle="" data-xl-buttonStyle="Standard" data-xl-fileName="Book1" data-xl-attribution="" ></a>
```


## <a name="workarounds"></a><span data-ttu-id="904e8-109">Problemumgehungen</span><span class="sxs-lookup"><span data-stu-id="904e8-109">Workarounds</span></span>

<span data-ttu-id="904e8-110">Alternativ empfehlen wir, [Excel in die Webseiten einzubetten ](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU).</span><span class="sxs-lookup"><span data-stu-id="904e8-110">We encourage you to  [embed Excel into your web pages ](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU) as an alternative.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="904e8-111">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="904e8-111">See also</span></span>
<span data-ttu-id="904e8-112"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="904e8-112"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="904e8-113">Excel Services in SharePoint</span><span class="sxs-lookup"><span data-stu-id="904e8-113">Excel Services in SharePoint</span></span>](excel-services-in-sharepoint.md)
    
  
-  [<span data-ttu-id="904e8-114">Einbetten einer Excel-Arbeitsmappe in Ihren Blog</span><span class="sxs-lookup"><span data-stu-id="904e8-114">Embed an Excel workbook on your blog</span></span>](https://support.office.com/en-au/article/Share-it-Embed-an-Excel-workbook-on-your-blog-804e1845-5662-487e-9b38-f96307144081?ui=en-US&amp;rs=en-AU&amp;ad=AU)
    
  

