---
title: "Erstellen von Websites für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 3b372a63-7cdf-462a-abb4-750e611e967d
ms.openlocfilehash: b6805fd65007827160720f8ad97b0401582edd80
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="build-sites-for-sharepoint"></a><span data-ttu-id="04970-102">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="04970-102">Build sites for SharePoint</span></span>
<span data-ttu-id="04970-103">Hier finden Sie Informationen zum neuen Websiteerstellungs- und Veröffentlichungsmodell für Websites in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="04970-103">Learn about the new site authoring and publishing model for websites in SharePoint.</span></span>
## <a name="introduction-to-site-publishing-for-designers-and-developers-in-sharepoint"></a><span data-ttu-id="04970-104">Einführung in die Websiteveröffentlichung für Designer und Entwickler in SharePoint</span><span class="sxs-lookup"><span data-stu-id="04970-104">Introduction to site publishing for designers and developers in SharePoint</span></span>
<span data-ttu-id="04970-105"><a name="SP15_BuildSitesForSP2013_IntroToSitePublishing"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-105"><a name="SP15_BuildSitesForSP2013_IntroToSitePublishing"> </a></span></span>

<span data-ttu-id="04970-p101">SharePoint führt ein Websiteerstellungs- und Veröffentlichungsmodell zur Erstellung von Veröffentlichungswebsites ein. Mithilfe von Veröffentlichungswebsites können Sie Inhalte auf Intranet- oder Internetsites veröffentlichen. Veröffentlichungswebsites unterscheiden sich von anderen Typen von SharePoint-Websites wie Teamsites hauptsächlich aufgrund ihres Zwecks: Viele Benutzer lesen Inhalte auf Veröffentlichungswebsites, aber nur wenige leisten einen Beitrag, indem sie Inhalte aus einer oder mehreren Websitesammlungen hinzufügen, aktualisieren und löschen. Im Gegensatz dazu stehen Teamwebsites, an denen möglicherweise viele Benutzer zusammenarbeiten und zu den Inhalten beitragen.</span><span class="sxs-lookup"><span data-stu-id="04970-p101">SharePoint introduces a site authoring and publishing model to create publishing sites. You can use publishing sites to publish content on intranet or Internet sites. Publishing sites differ from other types of SharePoint sites, such as team sites, mainly due to their purpose—many users read publishing site content, but only a few contribute by adding, updating, and deleting content from one or more site collections. Contrast these sites with team sites, where many people may collaborate and contribute to the content.</span></span> 
  
    
    
<span data-ttu-id="04970-p102">Sie können die Websiteveröffentlichungsfunktionen von SharePoint verwenden, um Veröffentlichungswebsites, die bestimmte Geschäftsanforderungen erfüllen, zu erstellen, anzupassen und zu verwalten. Ob Sie nun ein professioneller Webdesigner mit Kenntnissen in HTML, CSS und JavaScript oder ein Entwickler sind, der SharePoint-Apps schreibt und benutzerdefinierten .NET-Code verwendet, um Websites und Farmlösungen zu erstellen: Sie können mithilfe von Websitefeatures in SharePoint alle Phasen des Inhaltslebenszyklus verwalten. Dazu zählen:</span><span class="sxs-lookup"><span data-stu-id="04970-p102">You can use the SharePoint site publishing capabilities to build, customize, and maintain publishing sites that meet specific business needs. Whether you are a professional designer with HTML, CSS, and JavaScript skills or a developer who writes SharePoint apps and uses custom .NET code to build sites and farm solutions, you can use site features in SharePoint to manage all phases of the content life cycle, including:</span></span>
  
    
    

- <span data-ttu-id="04970-112">**Authoring** und Wiederverwenden von Websiteinhalten</span><span class="sxs-lookup"><span data-stu-id="04970-112">**Authoring** and reusing site content.</span></span>
    
  
- <span data-ttu-id="04970-113">**Branding** und Entwerfen des Aussehen und Verhaltens Ihrer Website</span><span class="sxs-lookup"><span data-stu-id="04970-113">**Branding** and designing your site's look, feel, and behavior.</span></span>
    
  
- <span data-ttu-id="04970-114">**Managing metadata** - Sie können ein taxonomiegesteuertes Websitenavigationssystem erstellen.</span><span class="sxs-lookup"><span data-stu-id="04970-114">**Managing metadata**—you can build a taxonomy-driven site navigation system.</span></span>
    
  
- <span data-ttu-id="04970-115">Problemloses **Publishing** von Inhalten in der aktuellen Websitesammlung oder Veröffentlichen von Inhalten in mehreren Websitesammlungen, auch über die Grenzen der Intranet- und Internetsite hinweg</span><span class="sxs-lookup"><span data-stu-id="04970-115">**Publishing** content smoothly to the current site collection, or publishing content across site collections—even spanning the intranet and Internet site boundary.</span></span>
    
  
- <span data-ttu-id="04970-116">**Accessibility** - Sie können die Barrierefreiheit Ihrer veröffentlichten Websites verbessern.</span><span class="sxs-lookup"><span data-stu-id="04970-116">**Accessibility**—you can use to improve the accessibility of your published sites.</span></span>
    
  
<span data-ttu-id="04970-117">Eine Zusammenfassung der Neuigkeiten für Designer und Entwickler von veröffentlichten Websites in SharePoint finden Sie unter  [Neuerung bei SharePoint-Websiteentwicklung](what-s-new-with-sharepoint-site-development.md).</span><span class="sxs-lookup"><span data-stu-id="04970-117">If you want to see a summary of what's new for designers and developers of publishing websites in SharePoint, see  [What's new with SharePoint site development](what-s-new-with-sharepoint-site-development.md).</span></span> 
  
    
    

## <a name="authoring-design-and-branding-in-sharepoint"></a><span data-ttu-id="04970-118">Erstellung, Entwurf und Branding in SharePoint</span><span class="sxs-lookup"><span data-stu-id="04970-118">Authoring, design, and branding in SharePoint</span></span>
<span data-ttu-id="04970-119"><a name="SP15_BuildSitesForSP2013_AuthoringDesignBranding"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-119"><a name="SP15_BuildSitesForSP2013_AuthoringDesignBranding"> </a></span></span>

<span data-ttu-id="04970-120">SharePoint bietet einen neuen Ansatz zum Entwerfen von Websites.</span><span class="sxs-lookup"><span data-stu-id="04970-120">SharePoint provides a new approach for designing websites.</span></span> <span data-ttu-id="04970-121">Der Workflow für die Erstellung von Inhalten wurde überarbeitet, sodass Sie Inhalt mit beliebigen Tools erstellen und großartige Inhalte erzeugen können.</span><span class="sxs-lookup"><span data-stu-id="04970-121">The content-creation workflow is revised so that you can create content using any —and author great content.</span></span> <span data-ttu-id="04970-122">Wenn Sie Ihre Website mit Branding versehen möchten, ohne benutzerdefinierten .NET-Code schreiben zu müssen, verwenden Sie den [Entwurfs-Manager](overview-of-design-manager-in-sharepoint.md) zum Importieren von Designelementen.</span><span class="sxs-lookup"><span data-stu-id="04970-122">To brand your site without having to write custom .NET code, use the  [Design Manager](overview-of-design-manager-in-sharepoint.md) to import design elements.</span></span> <span data-ttu-id="04970-123">Mit dem Entwurfs-Manager können Sie auch eine HTML-basierte Gestaltungsvorlage erstellen, um das allen Seiten Ihrer Website gemeinsame Chrom zu definieren und Seitenlayouts zum Entwerfen von Vorlagen für Seiten zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="04970-123">With Design Manager, you can also create an HTML-based master page to define the chrome shared by all of your site's pages and create page layouts to design templates for pages.</span></span> <span data-ttu-id="04970-124">Wenn Sie sich für das Schreiben von benutzerdefiniertem Code entscheiden, können Sie .NET-Server-, .NET-Client- (CSOM.md), Silverlight- und JavaScript-Bibliotheken verwenden.</span><span class="sxs-lookup"><span data-stu-id="04970-124">If you choose to write custom code, you can use .NET server, .NET client (CSOM.md), Silverlight, and JavaScript libraries.</span></span>
  
    
    
<span data-ttu-id="04970-p104">SharePoint bietet außerdem einen neuen Ansatz für Inhalte und deren Erstellung. Der Inhaltserstellungsworkflow wurde so überarbeitet, dass Sie mit jedem beliebigen Erstellungs- und Brandingtool tolle Inhalte erstellen können. Um Ihre Website mit Ihrem Branding zu versehen, ohne benutzerdefinierten ASP.NET-Code schreiben zu müssen, verwenden Sie den Entwurfs-Manager. Sie können Entwurfselemente importieren und eine HTML-basierte Gestaltungsvorlage erstellen, um die gemeinsamen Framingelemente, das Chrome, zu definieren, das alle Seiten und Seitenlayouts Ihrer Website verwenden. Wenn Sie benutzerdefinierten Code schreiben möchten, wenn Sie Ihre Website mit Ihrem Branding versehen, können Sie die Veröffentlichungs- und Taxonomiebibliotheken verwenden.</span><span class="sxs-lookup"><span data-stu-id="04970-p104">SharePoint also provides a new approach to content and authoring. The content-creation workflow is revised so that you can create content using any authoring and branding tool and author great content. To brand your site without having to write custom ASP.NET code, use the Design Manager. You can import design elements and create an HTML-based master page to define the shared framing elements—the chrome—that all of your site's pages and page layouts share. If you choose to write custom code when branding your site, you can use the publishing and taxonomy libraries.</span></span>
  
    
    

## <a name="publishing-sites-client-object-model-programming-and-the-new-sharepoint-app-model"></a><span data-ttu-id="04970-130">Veröffentlichen von Websites, Clientobjektmodell-Programmierung und das neue SharePoint-App-Modell</span><span class="sxs-lookup"><span data-stu-id="04970-130">Publishing sites, client object model programming, and the new SharePoint app model</span></span>
<span data-ttu-id="04970-131"><a name="SP15_BuildSitesForSP2013_PublishingSites"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-131"><a name="SP15_BuildSitesForSP2013_PublishingSites"> </a></span></span>

<span data-ttu-id="04970-p105">Sie können das neue .NET-Clientobjektmodell (CSOM) verwenden, um SharePoint-Apps mit dem Modell für SharePoint-Add-Ins zu entwickeln. Sie können viele der APIs verwenden, die auch für .NET-Serverprogrammierung in den .NET-Clientobjektmodellen verfügbar sind, die .NET client-, Silverlight-, JavaScript- und in einigen Fällen Windows Phone-Entwicklung unterstützen. Ideen für die Entwicklung von Apps für Websites sind etwa Umfragen, Kontoverwaltungs-Apps, E-Commerce-Support, Integration sozialer Features und externer Daten in Veröffentlichungswebsites, Hinzufügen outgesourcter Inhalte und mobile Begleit-Apps.</span><span class="sxs-lookup"><span data-stu-id="04970-p105">You can use the new .NET client object model (CSOM) to develop SharePoint apps with the model for SharePoint Add-ins. You can use many of the APIs that are also available for .NET server programming in the .NET client object models, which support .NET client, Silverlight, JavaScript—and in some cases Windows Phone—development. Some ideas for developing apps for websites include surveys, account management apps, eCommerce support, integrating social features and external data into publishing websites, outsourced content additions, and mobile companion apps.</span></span> 
  
    
    

## <a name="page-model-for-publishing-websites"></a><span data-ttu-id="04970-134">Seitenmodell für die Veröffentlichung von Websites</span><span class="sxs-lookup"><span data-stu-id="04970-134">Page model for publishing websites</span></span>
<span data-ttu-id="04970-135"><a name="SP15_BuildSitesForSP2013_PageModel"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-135"><a name="SP15_BuildSitesForSP2013_PageModel"> </a></span></span>

<span data-ttu-id="04970-p106">SharePoint enthält ein Seitenmodell für Veröffentlichungswebsites. Das Seitenmodell umfasst Gestaltungsvorlagen, Seitenlayouts und andere Komponenten, die die Struktur, die Inhalte, das Aussehen und das Verhalten Ihrer Website wiedergeben. Weitere Informationen finden Sie unter  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md).</span><span class="sxs-lookup"><span data-stu-id="04970-p106">SharePoint includes a page model for publishing websites. The page model includes master pages, page layouts, and other components that render your site structure, content, look and feel, and behavior. To learn more, see  [Overview of the SharePoint page model](overview-of-the-sharepoint-page-model.md).</span></span>
  
    
    

## <a name="master-pages-and-page-layouts"></a><span data-ttu-id="04970-139">Gestaltungsvorlagen und Seitenlayouts</span><span class="sxs-lookup"><span data-stu-id="04970-139">Master pages and page layouts</span></span>
<span data-ttu-id="04970-140"><a name="SP15_BuildSitesForSP2013_MasterAndLayout"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-140"><a name="SP15_BuildSitesForSP2013_MasterAndLayout"> </a></span></span>

<span data-ttu-id="04970-p107">Eine Gestaltungsvorlage ist die Hauptvorlage, welche die gemeinsam verwendeten strukturellen Elemente Ihrer Website definiert: das Chrome. Alle Seiten der Website verwenden diese Elemente gemeinsam, welche die Bereiche der Seite definieren, in denen Seitenlayoutinhalte angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="04970-p107">A master page is the main template that defines the shared structural elements of your site—the chrome. All of the pages on the site share these elements, which define the regions of the page that display page layout content.</span></span>
  
    
    
<span data-ttu-id="04970-p108">Seitenlayouts werden von einzelnen Seiten eines bestimmten Typs verwendet. Sie werden mit Anordnungen von Seitenfeldern aufgefüllt. Diese Seiten definieren einzelne Elemente auf der Seite. Einzelne Seiten basieren auf Seitenlayouts und werden in Ihrem Webbrowser entweder durch benutzerdefinierten Code oder dadurch erstellt, wie die Benutzer der Website die Felder der Seite ausfüllen. Weitere Informationen zum Seitenmodell in SharePoint finden Sie unter  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md).</span><span class="sxs-lookup"><span data-stu-id="04970-p108">Page layouts are used by individual pages of a certain type. They are populated with arrangements of page fields. These pages define individual elements on the page. Individual pages are based on page layouts and are created in your web browser either by custom code or by how the site's users fill out the page's fields. To learn more about the page model in SharePoint, see  [Overview of the SharePoint page model](overview-of-the-sharepoint-page-model.md).</span></span> 
  
    
    

## <a name="client-side-rendering-controls"></a><span data-ttu-id="04970-148">Clientseitige Rendering-Steuerelemente</span><span class="sxs-lookup"><span data-stu-id="04970-148">Client-side rendering controls</span></span>
<span data-ttu-id="04970-149"><a name="SP15_BuildSitesForSP2013_ClientSideRendering"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-149"><a name="SP15_BuildSitesForSP2013_ClientSideRendering"> </a></span></span>

<span data-ttu-id="04970-p109">Alle neuen Steuerelemente in SharePoint werden gerendert. Daten werden in die Steuerelemente in einem clientseitigen JSON-Array geschrieben, und Sie können Inhalte mithilfe von JavaScript, CSS und Vorlagen anzeigen. Als Webdesigner oder -entwickler können Sie steuern, wie Inhalte auf der Seite gerendert werden, und Sie können mithilfe von Features wie dem  [Inhaltssuche-Webpart in SharePoint](content-search-web-part-in-sharepoint.md) und Anzeigevorlagen verschiedene Entwurfstechniken verwenden, um auf Ihren veröffentlichten Seiten das gewünschte Aussehen und Verhalten zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="04970-p109">All new controls in SharePoint are rendered. Data is written to the controls in a client-side JSON array, and you can display content using JavaScript, CSS, and templates. As a designer or developer, you have control over how content is rendered on the page, and you can use various design techniques to get the look and behaviors you want on your published pages by using features like the  [Content Search Web Part in SharePoint](content-search-web-part-in-sharepoint.md) and display templates.</span></span>
  
    
    

## <a name="sites-and-mobile-devices"></a><span data-ttu-id="04970-153">Websites und mobile Geräte</span><span class="sxs-lookup"><span data-stu-id="04970-153">Sites and mobile devices</span></span>
<span data-ttu-id="04970-154"><a name="SP15_BuildSitesForSP2013_SitesAndMobile"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-154"><a name="SP15_BuildSitesForSP2013_SitesAndMobile"> </a></span></span>

<span data-ttu-id="04970-p110">Veröffentlichungswebsites in SharePoint sind für die Entwicklung mobiler Websites optimiert. Sie können Kanäle für ein oder mehrere Geräte (Gerätekanäle) definieren und für jeden Kanal eine alternative Gestaltungsvorlage und damit einzigartige strukturelle Elemente oder Chrome zuweisen. Sie können in einem Kanal Teile eines beliebigen Seitenlayouts ein- oder ausschließen, und während der Entwicklung in der Vorschau anzeigen, wie das mobile Kanaldesign verarbeitet wird.</span><span class="sxs-lookup"><span data-stu-id="04970-p110">Publishing websites in SharePoint are optimized for mobile development. You can define channels for one or more devices (device channels) and assign an alternate master page for each channel, giving it unique structural elements, or chrome. You can choose to include or exclude portions of any page layout in a channel, and preview how mobile channel design is progressing while it's being developed.</span></span> 
  
    
    

## <a name="metadata-and-navigation-in-sharepoint"></a><span data-ttu-id="04970-158">Metadaten und Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="04970-158">Metadata and navigation in SharePoint</span></span>
<span data-ttu-id="04970-159"><a name="SP15_BuildSitesForSP2013_MetadataNav"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-159"><a name="SP15_BuildSitesForSP2013_MetadataNav"> </a></span></span>

<span data-ttu-id="04970-p111">In Microsoft SharePoint Server 2010 eingeführte verwaltete Metadatenfunktionen wurden in SharePoint verbessert und erweitert. Sie bieten jetzt eine bessere Leistung, leichteren Zugriff über die Benutzeroberfläche und taxonomiegesteuerte Navigation, die als verwaltete Navigation bezeichnet wird. Sie können zur Erstellung Ihrer Websitenavigation verwaltete Navigation oder auf der SharePoint-Websitestruktur basierte Navigation, die alsstrukturierte Navigation bezeichnet wird, verwenden. Weitere Informationen zur verwalteten Navigation finden Sie unter [Verwaltete Metadaten und Navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint.md) und [Verwaltete Navigation in SharePoint](managed-navigation-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="04970-p111">Managed metadata capabilities introduced in Microsoft SharePoint Server 2010 are improved and extended in SharePoint for better performance, easier access through the user interface, and taxonomy-driven navigation—called managed navigation. You can use managed navigation or navigation based on the SharePoint website structure—called structured navigation—to build your site navigation. To learn more about managed navigation, see  [Managed metadata and navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint.md) and [Managed navigation in SharePoint](managed-navigation-in-sharepoint.md).</span></span>
  
    
    

## <a name="publishing-content-in-sharepoint"></a><span data-ttu-id="04970-163">Veröffentlichung von Inhalten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="04970-163">Publishing content in SharePoint</span></span>
<span data-ttu-id="04970-164"><a name="SP15_BuildSitesForSP2013_PublishingContent"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-164"><a name="SP15_BuildSitesForSP2013_PublishingContent"> </a></span></span>

<span data-ttu-id="04970-165">SharePoint bietet die folgenden neuen Inhaltsveröffentlichungsfeatures, mit denen Sie Veröffentlichungswebsites entwickeln können, die neue, flexiblere und komplexere Topologien und Szenarios mit größerer Barrirefreiheit unterstützen.</span><span class="sxs-lookup"><span data-stu-id="04970-165">SharePoint offers the following new content publishing features that enable you to develop publishing sites that support more flexible, more accessible, and more complex topologies and scenarios.</span></span> 
  
    
    

### <a name="catalogs"></a><span data-ttu-id="04970-166">Kataloge</span><span class="sxs-lookup"><span data-stu-id="04970-166">Catalogs</span></span>

<span data-ttu-id="04970-p112">SharePoint führt Kataloge ein, die Sie zum Veröffentlichen von Inhalten über Websitesammlungen hinweg verwenden können. Für Features zur websiteübergreifenden Veröffentlichung sind Kataloge erforderlich. Sie können sie verwenden, um Inhalte auf Ihren Websites und außerhalb der Grenzen zwischen Ihren Intranet- und Internetsites wiederzuverwenden. Für vordefinierte Suchanfragen werden Kataloge in der Suche markiert. Sie können in Katalogen gespeicherte Inhalte mithilfe des [Inhaltssuche-Webpart in SharePoint](content-search-web-part-in-sharepoint.md) in mehreren Websitesammlungen bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="04970-p112">SharePoint introduces catalogs, which you can use to publish content across site collections. Cross-site publishing features depend on catalogs. You can use them to reuse content across your sites and across the boundary between your intranet sites and Internet sites. For predefined search queries, catalogs are flagged in search. You can surface content stored in catalogs across site collections by using the  [Content Search Web Part in SharePoint](content-search-web-part-in-sharepoint.md).</span></span>
  
    
    

### <a name="cross-site-publishing"></a><span data-ttu-id="04970-172">Websiteübergreifende Veröffentlichung</span><span class="sxs-lookup"><span data-stu-id="04970-172">Cross-site publishing</span></span>

<span data-ttu-id="04970-p113">SharePoint führt ein neues Feature zur websiteübergreifenden Veröffentlichung ein, um Inhalte in mehreren Websitesammlungen wiederzuverwenden. Es verwendet integrierte Suchfunktionen, um Veröffentlichungsszenarios und -architekturen zu ermöglichen. Zum ersten Mal können Sie SharePoint-Farmen übergreifende Websites entwerfen, sodass Ihre Websites die Grenzen zwischen Intranets und dem Internet überspannen. Sie können das CSWP verwenden, um Suchdaten anzuzeigen, die aus verschiedenen Websites und Websitesammlungen veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="04970-p113">SharePoint introduces a cross-site publishing feature to reuse content across multiple site collections. It uses built-in search capabilities to enable publishing scenarios and architectures. For the first time, you can design sites that cross SharePoint farms—enabling your sites to span the boundary between intranets and the Internet. You can use the CSWP to display search data published from across sites and site collections.</span></span>
  
    
    

### <a name="variations-and-multilingual-sites"></a><span data-ttu-id="04970-177">Variationen und mehrsprachige Websites</span><span class="sxs-lookup"><span data-stu-id="04970-177">Variations and multilingual sites</span></span>

<span data-ttu-id="04970-178">Sie können das Variationsfeature in SharePoint verwenden, um mehrsprachige Websites oder andere Websites zu erstellen, auf denen Sie die Präsentation Ihrer Inhalte variieren möchten.</span><span class="sxs-lookup"><span data-stu-id="04970-178">You can use the variations feature in SharePoint to create multilingual sites or other sites where you want to vary the presentation of your content.</span></span> <span data-ttu-id="04970-179">Das Variationsfeature ist auf eine Websitesammlung beschränkt.</span><span class="sxs-lookup"><span data-stu-id="04970-179">The variations feature is constrained to one site collection.</span></span> <span data-ttu-id="04970-180">Das heißt, Sie können für eine Quellsprache/ein Quellgebietsschema mehrere Zielsprachen-/-gebietsschema-Varianten als aktuelle Websites innerhalb der gleichen SharePoint-Websitesammlung erstellen.</span><span class="sxs-lookup"><span data-stu-id="04970-180">That is, you can create target language/locale "variants" of a source language/locale as current websites within the same SharePoint site collection.</span></span> <span data-ttu-id="04970-181">Variationen unterstützen benutzerfreundliche URLs sowie die Möglichkeit zum Exportieren oder Importieren von Inhalten für die Übersetzung durch einen Drittanbieter im [XLIFF-Dateiformat](the-xliff-interchange-file-format-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="04970-181">Variations supports friendly URLs and the ability to export or import content for translation by a third party in  [XLIFF file format](the-xliff-interchange-file-format-in-sharepoint.md).</span></span> <span data-ttu-id="04970-182">Sie können Bezeichnungen, eine Seite für Übersetzung und Replikation, eine Vielzahl von Listenelementen (z. B. Dokumentbibliotheken.md) und Navigation in die Exportpakete einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="04970-182">You can include labels, a page for translation and replication, a variety of list items (for example, document libraries.md), and navigation in your export packages.</span></span> 
  
    
    

### <a name="accessible-sites"></a><span data-ttu-id="04970-183">Barrierefreie Websites</span><span class="sxs-lookup"><span data-stu-id="04970-183">Accessible sites</span></span>

<span data-ttu-id="04970-p115">Sie können das Variationsfeature in SharePoint verwenden, um barrierefreie Websites oder andere Websites zu erstellen, wenn Sie die Präsentation Ihrer Inhalte für Benutzer mit unterschiedlichen Anforderungen im Zusammenhang mit Barrierefreiheit anpassen möchten. SharePoint stellt einen "Zugriffsfreundlicheren Modus" bereit, der durch Öffnen einer SharePoint-Webseite und Drücken der TAB-Taste bis zu dem Link "Aktivieren des zugriffsfreundlicheren Modus" aktiviert werden kann. Dieses Feature erstellt die Webseite in standardmäßigen HTML-Code neu, wodurch sie für Bildschirmleseprogramme leichter zu lesen ist. Indem Sie sicherstellen, dass Benutzer die TAB-Taste drücken können, um auf diesen Link zu fokussieren, können Sie eine zugriffsfreundlichere Version Ihrer SharePoint-Webseite erstellen. Dies umfasst JavaScript-basierte Dropdownmenüs, die in Hyperlinklisten konvertiert werden, und Objekte werden in einfacheres HTML konvertiert, damit Bildschirmleseprogramme den Inhalt verstehen.</span><span class="sxs-lookup"><span data-stu-id="04970-p115">You can use the variations feature in SharePoint to create accessible sites or other sites where you want to adapt the presentation of your content for users who have a variety of accessability needs. SharePointprovides a "More Accessible Mode", which can be activated by opening a SharePoint webpage, and pressing the TAB key until you find the "Turn on More Accessible Mode" link. This feature recreates the webpage in standard HTML, making it friendlier for screen-readers. By ensuring that users are able to press the TAB key to focus on this link, you are able to create a more accessible version of your SharePoint webpage. This includes JavaScript-based drop-down menus being converted to hyperlink lists and objects are converted to simpler HTML to allow screen-readers to understand the content.</span></span> 
  
    
    

## <a name="see-also"></a><span data-ttu-id="04970-189">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="04970-189">See also</span></span>
<span data-ttu-id="04970-190"><a name="SP15_BuildSitesForSP2013_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="04970-190"><a name="SP15_BuildSitesForSP2013_AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="04970-191">Optimieren von SharePoint-Website zur Barrierefreiheit</span><span class="sxs-lookup"><span data-stu-id="04970-191">Optimize SharePoint site accessibility</span></span>](optimize-sharepoint-site-accessibility.md)
    
  
-  [<span data-ttu-id="04970-192">Einrichten einer allgemeinen Entwicklungsumgebung für SharePoint</span><span class="sxs-lookup"><span data-stu-id="04970-192">Set up a general development environment for SharePoint</span></span>](set-up-a-general-development-environment-for-sharepoint.md)
    
  
-  [<span data-ttu-id="04970-193">Neuerung bei SharePoint-Websiteentwicklung</span><span class="sxs-lookup"><span data-stu-id="04970-193">What's new with SharePoint site development</span></span>](what-s-new-with-sharepoint-site-development.md)
    
  
-  [<span data-ttu-id="04970-194">Übersicht über die minimale Strategie herunterladen</span><span class="sxs-lookup"><span data-stu-id="04970-194">Minimal Download Strategy overview</span></span>](minimal-download-strategy-overview.md)
    
  
-  [<span data-ttu-id="04970-195">Ändern von SharePoint-Komponenten für MDS</span><span class="sxs-lookup"><span data-stu-id="04970-195">Modify SharePoint components for MDS</span></span>](modify-sharepoint-components-for-mds.md)
    
  
-  [<span data-ttu-id="04970-196">Serverklassenbibliothek für Websites und Inhalte für SharePoint</span><span class="sxs-lookup"><span data-stu-id="04970-196">SharePoint Sites and Content server class library</span></span>](http://msdn.microsoft.com/library/8a93e838-234c-41d8-b990-7ac1a415dd5e%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="04970-197">Clientklassenbibliothek für Websites und Inhalte</span><span class="sxs-lookup"><span data-stu-id="04970-197">Sites and Content client class library</span></span>](http://msdn.microsoft.com/library/e6542022-a459-4c3b-aee0-e350c6397139%28Office.15%29.aspx)
    
  

