---
title: Inhaltssuche-Webpart in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 6fb4bf41-0846-4dca-ad9e-906afdfd3d2b
ms.openlocfilehash: 9585738005f8fb2ed7581ef8245b60c60c16ff5b
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="content-search-web-part-in-sharepoint"></a><span data-ttu-id="da577-102">Inhaltssuche-Webpart in SharePoint</span><span class="sxs-lookup"><span data-stu-id="da577-102">Content Search Web Part in SharePoint</span></span>

  
    
    
![Konzeptuelles Übersichtsthema](../images/mod_icon_badge_conoverview.png)
  
    
    

  
    
    

  
    
    
<span data-ttu-id="da577-104">Informationen zum Inhaltssuche-Webpart (CSWP) in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="da577-104">Learn about the Content Search Web Part (CSWP) in SharePoint.</span></span>
## <a name="introducing-the-content-search-web-part-cswp"></a><span data-ttu-id="da577-105">Einführung in das Inhaltssuche-Webpart (CSWP)</span><span class="sxs-lookup"><span data-stu-id="da577-105">Introducing the Content Search Web Part (CSWP)</span></span>
<span data-ttu-id="da577-106"><a name="SP15_CSWP_IntroducingCSWP"> </a></span><span class="sxs-lookup"><span data-stu-id="da577-106"><a name="SP15_CSWP_IntroducingCSWP"> </a></span></span>

<span data-ttu-id="da577-107">Das Inhaltssuche-Webpart (Content Search Web Part, CSWP) wurde in SharePoint eingeführt. Es verwendet verschiedene Optionen für die Formatierung, um dynamische Inhalte auf SharePoint-Seiten anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="da577-107">The Content Search Web Part (CSWP) is a Web Part introduced in SharePoint that uses various styling options to display dynamic content on SharePoint pages.</span></span>
  
    
    

## <a name="how-the-content-search-web-part-works"></a><span data-ttu-id="da577-108">Funktionsweise des Inhaltssuche-Webparts</span><span class="sxs-lookup"><span data-stu-id="da577-108">How the Content Search Web Part works</span></span>
<span data-ttu-id="da577-109"><a name="SP15_CSWP_HowCSWPWorks"> </a></span><span class="sxs-lookup"><span data-stu-id="da577-109"><a name="SP15_CSWP_HowCSWPWorks"> </a></span></span>

<span data-ttu-id="da577-p101">Das Inhaltssuche-Webpart zeigt Suchergebnisse in einer Weise an, die Sie einfach formatieren können. Jedem Inhaltssuche-Webpart ist eine Suchabfrage zugeordnet, für die die Ergebnisse angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="da577-p101">Content Search Web Part displays search results in a way that you can easily format. Each Content Search Web Part is associated with a search query and shows the results for that search query.</span></span>
  
    
    
<span data-ttu-id="da577-p102">Sie können Anzeigevorlagen verwenden, um die Darstellung der Suchergebnisse auf der Seite zu ändern. Anzeigevorlagen sind HTML- und JavaScript-Codeausschnitte zum Rendern der von SharePoint zurückgegebenen Informationen. Die anzuzeigenden Informationen werden im JSON-Format in die Seite eingefügt.</span><span class="sxs-lookup"><span data-stu-id="da577-p102">You can use display templates to change how search results appear on the page. Display templates are snippets of HTML and JavaScript that render the information returned by SharePoint. The information to be displayed gets inserted into the page in JSON format.</span></span> 
  
    
    

## <a name="when-to-use-the-content-search-web-part-cswp-or-the-content-query-web-part-cqwp"></a><span data-ttu-id="da577-115">Gründe für die Verwendung des Inhaltssuche-Webparts (CSWP) oder des Webparts für Inhaltsabfragen (CQWP)</span><span class="sxs-lookup"><span data-stu-id="da577-115">When to use the Content Search Web Part (CSWP) or the Content Query Web Part (CQWP)</span></span>
<span data-ttu-id="da577-116"><a name="SP15_CSWP_WhenToUseCSWPorCQWP"> </a></span><span class="sxs-lookup"><span data-stu-id="da577-116"><a name="SP15_CSWP_WhenToUseCSWPorCQWP"> </a></span></span>

<span data-ttu-id="da577-p103">Das Inhaltssuche-Webpart kann beliebige Inhalte aus dem Suchindex zurückgeben. Verwenden Sie es auf Ihren SharePoint-Websites, wenn Sie eine Verbindung mit einem Suchdienst herstellen und indizierte Suchergebnisse auf Ihren Seiten zurückgeben möchten.</span><span class="sxs-lookup"><span data-stu-id="da577-p103">The CSWP can return any content from the search index. Use it on your SharePoint sites when you are connecting to a search service and want to return indexed search results in your pages.</span></span> 
  
    
    
<span data-ttu-id="da577-p104">Das Inhaltssuche-Webpart gibt Inhalte zurück, die so aktuell sind wie die letzte Durchforstung Ihrer Inhalte. Wenn Sie häufig Durchforstungen ausführen, ist der vom Inhaltssuche-Webpart zurückgegebene Inhalt aktueller, als wenn Sie nur selten Durchforstungen ausführen. Wenn aktuelle Inhalte oder die aktualisierte Version der Inhalte angezeigt werden sollen, verwenden Sie stattdessen das Webpart für Inhaltsabfragen (Content Query Web Part, CQWP).</span><span class="sxs-lookup"><span data-stu-id="da577-p104">The CSWP returns content that is as fresh as the latest crawl of your content, so if you crawl often, the content that the CSWP returns is more up-to-date than if you crawl infrequently. If you need to display instant content or the refreshed version of content, use the Content Query Web Part (CQWP) instead.</span></span>
  
    
    
<span data-ttu-id="da577-p105">Bei der Suche werden nur die Hauptversionen von Inhalten durchforstet, niemals die Nebenversionen. Wenn Sie die Nebenversionen von Inhalten anzeigen möchten, verwenden Sie dazu ein Webpart für Inhaltsabfragen.</span><span class="sxs-lookup"><span data-stu-id="da577-p105">Search crawls only the major versions of content, never the minor versions. If you want to display the minor versions of your content, do that by using a CQWP.</span></span>
  
    
    
<span data-ttu-id="da577-p106">Einige Websitesammlungsadministratoren markieren Websites, die nicht indiziert werden sollen. So markierte Inhalte ist nicht in einem Inhaltssuche-Webpart verfügbar. Wenn Sie Ergebnisse aus einer Website zurückgeben möchten, die als nicht indizierbar gekennzeichnet ist, verwenden Sie das Webpart für Inhaltsabfragen.</span><span class="sxs-lookup"><span data-stu-id="da577-p106">Some site collection administrators mark sites to not be indexed. Content marked in this way is not available in a CSWP. If you want to return results from a site that is marked to not index, use the CQWP instead.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="da577-126">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="da577-126">Additional resources</span></span>
<span data-ttu-id="da577-127"><a name="SP15_CSWP_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="da577-127"><a name="SP15_CSWP_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="da577-128">Verwaltete Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="da577-128">Managed navigation in SharePoint</span></span>](managed-navigation-in-sharepoint.md)
    
  
-  [<span data-ttu-id="da577-129">What's new in SharePoint-Suche für Entwickler</span><span class="sxs-lookup"><span data-stu-id="da577-129">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  

