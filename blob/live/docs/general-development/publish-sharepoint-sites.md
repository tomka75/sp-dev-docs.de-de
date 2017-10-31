---
title: "Veröffentlichen von SharePoint-Websites"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 46b5a79c-962f-4a07-8316-d5005eabd0e0
ms.openlocfilehash: 499e42a703295db74702751f607e2b41fc7c04d5
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="publish-sharepoint-sites"></a><span data-ttu-id="33d32-102">Veröffentlichen von SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="33d32-102">Publish SharePoint sites</span></span>

<span data-ttu-id="33d32-103">Nachdem Sie entwerfen oder Websitekomponenten und Inhalt zu entwickeln, können Sie diese stellen diese in der aktuellen Websitesammlung und andere Websitesammlungen - auch für Websitesammlungen, die das Intranet/Internetgrenze schneidet.</span><span class="sxs-lookup"><span data-stu-id="33d32-103">After you design or develop site components and content, you can deploy them to the current site collection and other site collections—even to site collections that cross the intranet/Internet boundary.</span></span>
  
    
    


## <a name="cross-site-publishing"></a><span data-ttu-id="33d32-104">Websiteübergreifende Veröffentlichung</span><span class="sxs-lookup"><span data-stu-id="33d32-104">Cross-site publishing</span></span>

<span data-ttu-id="33d32-105">Informationen Sie über  [websiteübergreifende Veröffentlichung](cross-site-publishing-in-sharepoint.md) und wie wirkt wie planen und Veröffentlichen von Websites und deren Inhalte und zugehörige Designelemente.</span><span class="sxs-lookup"><span data-stu-id="33d32-105">Learn about  [cross-site publishing](cross-site-publishing-in-sharepoint.md) and how it affects how you plan and publish sites and their content and associated design elements.</span></span>
  
    
    

## <a name="publishing-considerations-for-variations-and-multilingual-sites"></a><span data-ttu-id="33d32-106">Veröffentlichen von Überlegungen für Variationen und mehrsprachige Websites</span><span class="sxs-lookup"><span data-stu-id="33d32-106">Publishing considerations for variations and multilingual sites</span></span>

<span data-ttu-id="33d32-p101">Verschiedene Märkten haben verschiedene Geschmack. Das Variationsfeature unterstützt diesen Geschmack stellen bereit, mit denen Sie lokalisieren und Inhalte zu übersetzen, sondern auch Veröffentlichen dieser Inhalte und dessen zugehörige Designelemente für Websitesammlungen auf der ganzen Welt, aufzunehmen. Mit denen die Veröffentlichung von Inhalten in lokalen Märkten Erfolg zu machen, sollten Sie die folgenden Tipps, die zeigen, wie Entwurf und Inhalte Entscheidungen bezüglich der, die Sie vornehmen können beeinflussen wie veröffentlichten Websiteinhalt und Struktur rendern kann:</span><span class="sxs-lookup"><span data-stu-id="33d32-p101">Different markets have different tastes. The variations feature helps accommodate those tastes by providing functionality that you can use to localize and translate content, but also to publish that content and its associated design elements to site collections all over the world. To help make publishing content to local markets successful, consider these tips that show how design and content management decisions you make can affect how published site contents and structure may render:</span></span>
  
    
    

- <span data-ttu-id="33d32-p102">Duplizierung der Entwurfsressourcen positiv wirkt sich auf die Leistung der Website veröffentlichen und Rendern und stellt, Verwalten von komplexen Websites, die für Variationen weniger komplexen aktiviert sind. Eine Gestaltungsvorlage ist eine ASP.NET-Datei, die Inhaltsplatzhalter enthält, die durch Seitenlayouts und Seiten einzelne Instanzen aufgefüllt werden.</span><span class="sxs-lookup"><span data-stu-id="33d32-p102">Duplication of design assets positively affects the performance of site publishing and rendering and helps make managing complex sites that are enabled for variations less complex. A master page is an ASP.NET file that contains content placeholders that are populated by page layouts and individual instances of pages.</span></span> 
    
  
- <span data-ttu-id="33d32-p103">Wenn bestimmte Inhaltstypen für alle Gebietsschemas in Ihrer Websitesammlung anwenden, empfiehlt es sich als Website Inhaltstypen des Stammwebs erstellt. Sie können auch unter Variationswebsites Inhaltstypen erstellen.</span><span class="sxs-lookup"><span data-stu-id="33d32-p103">If certain content types apply to all locales in your site collection, it's best to create them as site content types of the root web. You can also create content types under variation sites.</span></span> 
    
  
- <span data-ttu-id="33d32-114">Wenn Sie zusätzliche Spalten hinzufügen einer Quellliste durch Hinzufügen eines Elements zu einem Inhaltstyp, der zuvor nicht in dieser Liste vorhanden war, Variationen aktualisiert das Schema der einzelnen Zielliste entsprechend die neuen Spalten das nächste Mal dieser Zielliste ein Element hinzu.</span><span class="sxs-lookup"><span data-stu-id="33d32-114">If you add additional columns to a source list by adding an item with a content type that did not previously exist in that list, variations updates the schema of each target list to reflect the new columns the next time you add an item to that target list.</span></span> 
    
  
- <span data-ttu-id="33d32-p104">Verwaltete Navigation arbeitet mit Variationen. Strukturierte Navigation - basierend auf der SharePoint-Website-Struktur - auch noch funktioniert: Es Inhalt und Struktur zwischen den Quell- und Variationen Etiketten synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="33d32-p104">Managed navigation works with variations. Structured navigation—based on the SharePoint website structure—also still works: it synchronizes the content and structure between the source and target variations labels.</span></span> 
    
  
- <span data-ttu-id="33d32-p105">Das Gerät Kanäle Feature abstrahiert das Problem die Präsentation von Inhalten für mobile Geräte aus der zugrunde liegenden Websiteinhalt und-Struktur variieren. Sie können auf Masterseiten erstellen, die den Benutzern basierend auf Benutzer-Agent des Benutzers angezeigt. Vermeiden Sie hartcodierten in eine Gestaltungsvorlage Inhalte, die lokalisiert werden muss.</span><span class="sxs-lookup"><span data-stu-id="33d32-p105">The device channels feature abstracts the problem of varying the presentation of content for mobile devices from the underlying site content and structure. You can create master pages that present to users based on the user's user agent. Avoid hard-coding in a master page content that will need to be localized.</span></span>
    
  
- <span data-ttu-id="33d32-p106">Websites mit dynamischen Inhalt zusammengestellt aus mehreren Quellen Risiko müssen Inhalte in mehreren Sprachen auf derselben Seite gerendert wurde. Vermeiden Sie beispielsweise Fällen, in denen Artikel Seiteninhalt einer Sprache während Inhalt gerendert, indem eine Inhalt-Webpart in eine andere Sprache gerendert werden.</span><span class="sxs-lookup"><span data-stu-id="33d32-p106">Sites with dynamic content assembled from multiple sources risk having content rendered in multiple languages on the same page. For example, avoid cases where article page content is one language while content rendered by a Content Search Web Part is rendered in another language.</span></span> 
    
  
- <span data-ttu-id="33d32-p107">Bei der Arbeit mit Anzeigevorlagen, die mit mehreren Sprachen verwendet werden, erstellen Sie Sprachdateien, und platzieren Sie diese unter-Ordner, die mit dem Gebietsschema, denen sie lauten auf anwenden. Sie können dann die Sprachdateien mit der  `$includeLanguageScript` -Funktion und das Token `{Locale}` verweisen.</span><span class="sxs-lookup"><span data-stu-id="33d32-p107">If you work with display templates that are used with multiple languages, create language files and place them under folders that are named with the locale that they apply to. You can then reference the language files with the  `$includeLanguageScript` function and the `{Locale}` token.</span></span>
    
    <span data-ttu-id="33d32-124">Wenn die Inhaltssuche-Webpart die **Language** -Eigenschaft beim Suchen der entsprechenden Datei CustomStrings.js nutzt enthalten eine ist nicht vorhanden, und Code in der Vorlage eine Zeichenfolge, die fordert mithilfe der Funktionen `$resource()` oder `Srch.U.loadResource()` nicht gefunden werden kann, um anzuzeigen, wird die Inhaltssuche-Webpart eine Fehlermeldung angezeigt.</span><span class="sxs-lookup"><span data-stu-id="33d32-124">If the Content Search Web Part relies on the **Language** property to find the appropriate CustomStrings.js file to include and one doesn't exist, and code in the template requests a string to display that cannot be found by using the `$resource()` or `Srch.U.loadResource()` functions, the Content Search Web Part displays an error message.</span></span>
    
  

## <a name="additional-resources"></a><span data-ttu-id="33d32-125">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="33d32-125">Additional resources</span></span>
<span data-ttu-id="33d32-126"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="33d32-126"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="33d32-127">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="33d32-127">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="33d32-128">Neuerung bei SharePoint-Websiteentwicklung</span><span class="sxs-lookup"><span data-stu-id="33d32-128">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  

