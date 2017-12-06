---
title: Optimieren der Leistung in SharePoint Seite
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 262caeef-64fd-4e02-b947-d772faf01159
ms.openlocfilehash: 6600de1925c934868941c5af3789e680d67c0569
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="optimize-page-performance-in-sharepoint"></a><span data-ttu-id="028cc-102">Optimieren der Leistung von Seiten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="028cc-102">Optimize page performance in SharePoint</span></span>
<span data-ttu-id="028cc-103">Erhalten Sie Informationen zu Features, mit denen Sie die Leistung von Seiten in SharePoint verbessern können.</span><span class="sxs-lookup"><span data-stu-id="028cc-103">Learn about features to improve performance in pages in SharePoint. These features can be used to enhance the experience in geographically distributed implementations.</span></span> <span data-ttu-id="028cc-104">Diese Features können verwendet werden, um die Erfahrung in geografisch verteilten Implementierungen zu verbessern.</span><span class="sxs-lookup"><span data-stu-id="028cc-104">Learn about features to improve performance in pages in SharePoint. These features can be used to enhance the experience in geographically distributed implementations.</span></span>
 <span data-ttu-id="028cc-105">**Zur Verfügung gestellt von:** David Crawford, Microsoft Corporation</span><span class="sxs-lookup"><span data-stu-id="028cc-105">**Provided by:** David Crawford, Microsoft Corporation</span></span>
  
    
    

<span data-ttu-id="028cc-p102">Dieser Artikel enthält Anweisungen, die Optimierung der Leistung in SharePoint helfen. SharePoint enthält Funktionen zur Seite laden über einen Bereich WAN (Wide Network) zu optimieren. Entwerfen von Seiten zu als kleine und schnell wie möglich ergänzt diese Leistungssteigerungen machen.</span><span class="sxs-lookup"><span data-stu-id="028cc-p102">This article provides instructions that will help optimize performance in SharePoint. SharePoint includes features that help optimize page loading over a Wide Area Network (WAN). Designing pages to make them as small and responsive as possible complements these performance improvements.</span></span>
## <a name="minimal-download-strategy-mds"></a><span data-ttu-id="028cc-109">Minimale Downloadstrategie (MDS)</span><span class="sxs-lookup"><span data-stu-id="028cc-109">Minimal Download Strategy (MDS)</span></span>
<span data-ttu-id="028cc-110"><a name="MDS"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-110"></span></span>

<span data-ttu-id="028cc-p103">Minimale herunterladen Strategie (MDS) nutzt die Möglichkeit, nur bestimmte Teile einer Seite herunterladen, die auf dem Server vollständig gerendert wird. Nur der bestimmte Teile herunterladen bietet ein sehr effizient Loading-Modell. Die vollständig gerenderte Seite wird nicht an den Client zurückgegeben. Der Server muss genau jene identifizieren, die sein müssen als Teil der Antwort und die, die nicht erforderlich sind. Die Teile, die möglicherweise nicht Teil der Antwort enthalten Skripts, Stile und Markup.</span><span class="sxs-lookup"><span data-stu-id="028cc-p103">Minimal Download Strategy (MDS) relies on the ability to download only specific portions of a page that is rendered fully on the server. Downloading only the specific portions provides a very efficient loading model. The fully rendered page is not returned to the client. The server must be able to accurately identify those pieces that must be part of the response and those that are not necessary. The pieces that may or may be not part of the response include scripts, styles, and markup.</span></span>
  
    
    
<span data-ttu-id="028cc-116">Die folgende Tabelle enthält einige Vorteile der Verwendung von MDS.</span><span class="sxs-lookup"><span data-stu-id="028cc-116">The following table shows some benefits of using MDS.</span></span>
  
    
    

<span data-ttu-id="028cc-117">**In Tabelle 1. Vorteile der Verwendung von MDS**</span><span class="sxs-lookup"><span data-stu-id="028cc-117">**Table 1. Benefits of using MDS**</span></span>


|<span data-ttu-id="028cc-118">**Leistung**</span><span class="sxs-lookup"><span data-stu-id="028cc-118">**Performance**</span></span>|<span data-ttu-id="028cc-119">**Visuelle Objekte**</span><span class="sxs-lookup"><span data-stu-id="028cc-119">**Visuals**</span></span>|
|:-----|:-----|
|<span data-ttu-id="028cc-120">Weniger Datenmengen pro Seitenanforderung heruntergeladen haben.</span><span class="sxs-lookup"><span data-stu-id="028cc-120">Fewer amounts of data downloaded per page request.</span></span>  <br/> |<span data-ttu-id="028cc-121">Keine Browser blinken zurückzuführen ganze Seite neu zu laden.</span><span class="sxs-lookup"><span data-stu-id="028cc-121">No browser flashing caused by full page reload.</span></span>  <br/> |
|<span data-ttu-id="028cc-122">Browser muss nur die Bereiche der Seite aktualisieren, die seit der letzten Anforderung geändert.</span><span class="sxs-lookup"><span data-stu-id="028cc-122">Browser needs to update only the regions of the page that changed since the last request.</span></span>  <br/> |<span data-ttu-id="028cc-123">Leicht zu identifizieren, Animationen.</span><span class="sxs-lookup"><span data-stu-id="028cc-123">Easy to identify animations.</span></span>  <br/> |
|<span data-ttu-id="028cc-124">Geringer Verarbeitungsaufwand auf dem Client erforderlich.</span><span class="sxs-lookup"><span data-stu-id="028cc-124">Small amount of processing required on the client.</span></span>  <br/><span data-ttu-id="028cc-125">**Hinweis:** Die Hälfte der Client-Seitenladezeit 1 (PLT1) wird für das Chrome-Cascading-Stylesheet-Rendering (CSS) und die Analyse und Ausführung von JavaScript benötigt.</span><span class="sxs-lookup"><span data-stu-id="028cc-125">Half of client Page-Load-Time 1 (PLT1) is due to chrome cascading style sheet (CSS) rendering and JavaScript parsing and execution.</span></span>           |<span data-ttu-id="028cc-126">Änderungen an der Seite wecken die Aufmerksamkeit des Benutzers.</span><span class="sxs-lookup"><span data-stu-id="028cc-126">Changes in the page attract user's attention.</span></span>  <br/> |
   
<span data-ttu-id="028cc-p104">AJAX und MDS sind Technologien, die nur Abschnitte der Seite, um Daten zu minimieren herunterladen und Verbesserung der Seite Reaktionsfähigkeit anfordern. Die folgende Abbildung zeigt die MDS-Architektur.</span><span class="sxs-lookup"><span data-stu-id="028cc-p104">Both AJAX and MDS are technologies that request only sections of the page to minimize data download and improve page responsiveness. The following figure shows the MDS architecture.</span></span>
  
    
    

<span data-ttu-id="028cc-129">**Abbildung 1. MDS-Architektur**</span><span class="sxs-lookup"><span data-stu-id="028cc-129">**Figure 1. MDS architecture**</span></span>

  
    
    

  
    
    
![MDS-Architektur](../images/OptimizePage_Fig01_MDSArchitecture.png)
  
    
    
<span data-ttu-id="028cc-p105">Das MDS-Framework wird davon ausgegangen, dass eine Gestaltungsvorlage Chrom und Inhaltsbereiche definiert. MDS bedeutet SharePoint Navigieren zu einer Seite anfordern nur den Inhalt für diesen Regionen und die Ressourcen, denen auf die Seite abhängig ist. Sobald dieser Inhalte an den Browser downloads, gilt Skriptcode die Markup oder Ressourcen auf der Seite aus. Der Browser verhält sich, als ob die angeforderte Seite vollständig vom Server geladen wurde, hatte.</span><span class="sxs-lookup"><span data-stu-id="028cc-p105">The MDS framework assumes that a master page defines a chrome and content regions. In MDS, SharePoint navigating to a page means requesting just the content for those regions and the resources that the page depends on. Once that content downloads to the browser, script code applies the markup or resources to the page as appropriate. The browser behaves as if the requested page had been loaded completely from the server.</span></span>
  
    
    

<span data-ttu-id="028cc-135">**Abbildung 2. Seitenchrom und Regionen in einer SharePoint-Seite**</span><span class="sxs-lookup"><span data-stu-id="028cc-135">**Figure 2. Page chrome and regions in a SharePoint page**</span></span>

  
    
    

  
    
    
![Seitenchrom und Regionen auf einer SharePoint-Seite](../images/OptimizePage_Fig02_PageStructure.png)
  
    
    
<span data-ttu-id="028cc-p106">Wenn Benutzer eine SharePoint-Website im Modus MDS durchsuchen, sie verursachen keine ganze Seitenpostbacks und ganze Seite neu geladen. Stattdessen die URL für die Seite ihnen besuchten erhalten bleibt, und der Fragmentbezeichner ("#"-Zeichen) ändert sich, um die Seite enthalten, die sie besuchen. Das Format der URL lautet:  `[Path to site (spweb)] + /_layouts/15/start.aspx# + [path to page] + [query string]`</span><span class="sxs-lookup"><span data-stu-id="028cc-p106">When users are browsing a SharePoint website in MDS mode, they will not cause full page postbacks and full page reloads. Instead, the URL for the page they are visiting will remain the same, and the fragment identifier (a "#"sign) will change to contain the page they are visiting. The format of the URL is:  `[Path to site (spweb)] + /_layouts/15/start.aspx# + [path to page] + [query string]`</span></span>
  
    
    
<span data-ttu-id="028cc-140">Die folgende Tabelle enthält einige Beispiele von URLs im Modus MDS formatiert.</span><span class="sxs-lookup"><span data-stu-id="028cc-140">The following table shows some examples of URLs formatted in MDS mode.</span></span>
  
    
    

<span data-ttu-id="028cc-141">**In Tabelle 2. URLs im Modus MDS formatiert**</span><span class="sxs-lookup"><span data-stu-id="028cc-141">**Table 2. URLs formatted in MDS mode**</span></span>


|<span data-ttu-id="028cc-142">**Nicht MDS-URL**</span><span class="sxs-lookup"><span data-stu-id="028cc-142">**Non-MDS URL**</span></span>|<span data-ttu-id="028cc-143">**MDS-URL**</span><span class="sxs-lookup"><span data-stu-id="028cc-143">**MDS URL**</span></span>|
|:-----|:-----|
|<span data-ttu-id="028cc-144">http://server/SitePages/</span><span class="sxs-lookup"><span data-stu-id="028cc-144">http://server/SitePages/</span></span>  <br/> |<span data-ttu-id="028cc-145">http://server/_layouts/15/start.aspx#/SitePages/</span><span class="sxs-lookup"><span data-stu-id="028cc-145">http://server/_layouts/15/start.aspx#/SitePages/</span></span>  <br/> |
|<span data-ttu-id="028cc-146">http://server/subsite/SitePages/home.aspx</span><span class="sxs-lookup"><span data-stu-id="028cc-146">http://server/subsite/SitePages/home.aspx</span></span>  <br/> |<span data-ttu-id="028cc-147">http://server/subsite/_layouts/15/start.aspx#/SitePages/home.aspx</span><span class="sxs-lookup"><span data-stu-id="028cc-147">http://server/subsite/_layouts/15/start.aspx#/SitePages/home.aspx</span></span>  <br/> |
|<span data-ttu-id="028cc-148">http://server/_layouts/15/viewlsts.aspx?BaseType=0</span><span class="sxs-lookup"><span data-stu-id="028cc-148">http://server/_layouts/15/viewlsts.aspx?BaseType=0</span></span>  <br/> |<span data-ttu-id="028cc-149">http://server/_layouts/15/start.aspx#/_layouts/viewlsts.aspx?BaseType=0</span><span class="sxs-lookup"><span data-stu-id="028cc-149">http://server/_layouts/15/start.aspx#/_layouts/viewlsts.aspx?BaseType=0</span></span>  <br/> |
   
<span data-ttu-id="028cc-p107">Das Objekt für die AJAX-Navigation verwendet wird, **AjaxNavigate**. Standardmäßig ist eine Instanz des **AjaxNavigate** für die Verwendung von benannten **ajaxNavigate**verfügbar. So verwenden Sie die Instanz **ajaxNavigate**</span><span class="sxs-lookup"><span data-stu-id="028cc-p107">The object used for the AJAX navigation is **AjaxNavigate**. By default, there is an instance of **AjaxNavigate** available for you to use named **ajaxNavigate**. To use the **ajaxNavigate** instance:</span></span>
  
    
    



```cs

ajaxNavigate.update(serverRelativeURL, null);
```

<span data-ttu-id="028cc-153">Wenn Sie möchten, dass ein Steuerelement oder Webpart Navigationsereignisse abhört, können Sie den Handler **Navigieren\_hinzufügen** verwenden.</span><span class="sxs-lookup"><span data-stu-id="028cc-153">If you want a control or Web Part to listen to the navigation events, you can use the **add\_navigate** handler.</span></span> <span data-ttu-id="028cc-154">Wenn der Handler aufgerufen wird, erhält Ihre Rückruffunktion einen Verweis auf das Navigationsobjekt und die analysierten Hash-Werte in einem Wörterbuch.</span><span class="sxs-lookup"><span data-stu-id="028cc-154">When the handler is called, your callback function receives a reference to the navigation object and the parsed hash values in a dictionary.</span></span> <span data-ttu-id="028cc-155">Das Steuerelement oder Webpart kann den Wert für den entsprechenden Parameter aus dem Wörterbuch abrufen, ihn mit dem aktuellen Wert vergleichen und entscheiden, welche Aktion ausgeführt werden muss.</span><span class="sxs-lookup"><span data-stu-id="028cc-155">The control or Web Part can retrieve the value for the parameter of interest from the dictionary, compare it to the current value, and decide what action it needs to take.</span></span> <span data-ttu-id="028cc-156">Eine häufige Aktion besteht darin, eine AJAX-Anforderung an den Server zum Abrufen von Daten zu senden oder die Elemente in der Ansicht neu anzuordnen.</span><span class="sxs-lookup"><span data-stu-id="028cc-156">A common action is to send an AJAX request to the server to retrieve some data or reorder the items in the view.</span></span> <span data-ttu-id="028cc-157">Wenn ein Steuerelement die Navigationsereignisse abgehört hat, können kann es den **Navigieren\_löschen**-Handler verwenden.</span><span class="sxs-lookup"><span data-stu-id="028cc-157">When a control has finished listening to navigation events, it can use the **remove\_navigate** handler.</span></span>
  
    
    
<span data-ttu-id="028cc-p109">MDS unterstützt auch mehrere Rauten in Schlüssel/Wert-Paare. MDS fügt die Rauten hinter dem URL an. Das Format der Rauten in der URL lautet: http://server/_layouts/15/start.aspx#/SitePages/page.aspx#key1=value1#key2=value2. Im folgenden Codebeispiel wird veranschaulicht, wie die Rauten aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="028cc-p109">MDS also supports multiple hash marks in key/value pairs. MDS appends the hash marks after the URL. The format of hash marks in the URL is: http://server/_layouts/15/start.aspx#/SitePages/page.aspx#key1=value1#key2=value2. The following code example shows how to update the hash marks.</span></span>
  
    
    



```
var updateParts;
updateParts = {key1: "value1", key2: "value2", keyn: "valuen"}
ajaxNavigate.update(null, updateParts);

```

<span data-ttu-id="028cc-p110">Wenn Sie feststellen, dass die Seiten in Ihrer Website ständig zurückgreifen, um die ganze Seite herunterladen, empfiehlt es sich, deaktivieren das Feature MDS berücksichtigt werden sollten. Sie sollten auch die MDS-Feature zu deaktivieren, wenn Sie eine andere Strategie zum Verbessern der Leistung verwenden müssen.</span><span class="sxs-lookup"><span data-stu-id="028cc-p110">If you find that the pages in your website constantly fall back to download the full page, you might want to consider turning the MDS feature off. You might also want to turn the MDS feature off if you need to use a different strategy to improve performance.</span></span>
  
    
    
<span data-ttu-id="028cc-p111">Ein bestimmtes Element in der Seite muss sicherstellen, dass die wichtigen Ressourcen für das Arbeiten mit der MDS-Infrastruktur zur Renderzeit Server bekannt sind. Um ein vorhandenes Projekt zu verwenden, MDS zu konvertieren, müssen Sie die folgenden Dateien und Komponenten aktualisieren:</span><span class="sxs-lookup"><span data-stu-id="028cc-p111">A particular element in the page must make sure that the critical resources needed to work are known to the MDS infrastructure at server rendering time. To convert an existing project to use MDS, you need to update the following files and components:</span></span>
  
    
    

- <span data-ttu-id="028cc-166">Gestaltungsvorlagen</span><span class="sxs-lookup"><span data-stu-id="028cc-166">Master pages</span></span>
    
  
- <span data-ttu-id="028cc-167">ASP.NET Seiten</span><span class="sxs-lookup"><span data-stu-id="028cc-167">ASP.NET pages</span></span>
    
  
- <span data-ttu-id="028cc-168">Benutzerdefinierte Masterseiten für Fehler</span><span class="sxs-lookup"><span data-stu-id="028cc-168">Custom master pages for errors</span></span>
    
  
- <span data-ttu-id="028cc-169">JavaScript-Dateien</span><span class="sxs-lookup"><span data-stu-id="028cc-169">JavaScript files</span></span>
    
  
- <span data-ttu-id="028cc-170">Steuerelemente und Webparts</span><span class="sxs-lookup"><span data-stu-id="028cc-170">Controls and Web Parts</span></span>
    
  

### <a name="master-pages"></a><span data-ttu-id="028cc-171">Gestaltungsvorlagen</span><span class="sxs-lookup"><span data-stu-id="028cc-171">Master pages</span></span>

<span data-ttu-id="028cc-p112">Die wichtigste Änderung in der Gestaltungsvorlage ist die Bereiche der HTML-Markup umgeben werden, die mit einem speziellen-Steuerelement mit dem Namen **SharePoint:AjaxDelta** an den Client gesendet wird. Die am häufigsten verwendeten Teile, die von einem Steuerelement **SharePoint:AjaxDelta** umgeben sein müssen, sind in der Gestaltungsvorlage Chrome und der Content Platzhalter eingebettet. Wenn ein Steuerelement auf allen Seiten innerhalb einer Website identisch ist, sollten sie nicht von einem Steuerelement **SharePoint:AjaxDelta** eingeschlossen werden. Das folgende Markup zeigt einen sichtbaren Inhaltsplatzhalter, umgeben von einer **SharePoint:AjaxDelta** -Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="028cc-p112">The main change in the master page is to surround the regions of HTML markup that will be sent to the client with a special control named **SharePoint:AjaxDelta**. The most common parts that need to be surrounded by a **SharePoint:AjaxDelta** control are the controls embedded in the master page chrome and the content place holders. If a control is the same on all pages within a site, it should not be wrapped by a **SharePoint:AjaxDelta** control. The following markup shows a visible content placeholder surrounded by a **SharePoint:AjaxDelta** control.</span></span>
  
    
    

```HTML

<SharePoint:AjaxDelta id="DeltaPlaceHolderMain" IsMainContent="true" runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderMain" runat="server" />
</SharePoint:AjaxDelta>
```

<span data-ttu-id="028cc-p113">Steuerelemente, die abhängig von der aktuellen URL Inhalt aufweisen müssen in einem Steuerelement **SharePoint:AjaxDelta** umbrochen werden. Das folgende Markup zeigt ein Menü, umgeben von einer **SharePoint:AjaxDelta** -Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="028cc-p113">Controls that have content dependent on the current URL must be wrapped in a **SharePoint:AjaxDelta** control. The following markup shows a menu surrounded by a **SharePoint:AjaxDelta** control.</span></span>
  
    
    



```HTML

<SharePoint:AjaxDelta id="DeltaBreadcrumbDropdown" runat="server">
    <SharePoint:PopoutMenu
        runat="server"
        ID="GlobalBreadCrumbNavPopout"
        IconUrl=IMGCLUSTER_FG_IMG
        IconAlt=LOC_ATTR_WSS(master_breadcrumbIconAlt)
        IconOffsetX=IMGCLUSTER_FG_LEFT(BREADCRUMBBUTTON)
        IconOffsetY=IMGCLUSTER_FG_TOP(BREADCRUMBBUTTON)
        IconWidth=IMGCLUSTER_FG_WIDTH(BREADCRUMBBUTTON)
        IconHeight=IMGCLUSTER_FG_HEIGHT(BREADCRUMBBUTTON)
        AnchorCss="s4-breadcrumb-anchor"
        AnchorOpenCss="s4-breadcrumb-anchor-open"
        MenuCss="s4-breadcrumb-menu">
    </SharePoint:PopoutMenu>
</SharePoint:AjaxDelta>

```


> <span data-ttu-id="028cc-178">**Hinweis:** Das **SharePoint: Ajaxdelta**-Steuerelement sollte nicht in sich selbst verschachtelt werden.</span><span class="sxs-lookup"><span data-stu-id="028cc-178">**Note** The **SharePoint:AjaxDelta** control should not be nested within itself. Specify this control at the highest required level.</span></span> <span data-ttu-id="028cc-179">Geben Sie dieses Steuerelement auf der höchsten erforderlichen Ebene an.</span><span class="sxs-lookup"><span data-stu-id="028cc-179">Note The SharePoint:AjaxDelta control should not be nested within itself. Specify this control at the highest required level.</span></span>
  
    
    

<span data-ttu-id="028cc-p115">Wenn Sie eine Datei cascading Stylesheet (CSS) einschließen möchten, müssen Sie die Steuerelemente **SharePoint:CssLink** und **SharePoint:CssRegistration** verwenden. Diese Steuerelemente wurden aktualisiert, um MDS und nicht MDS-Modus zu arbeiten. Das folgende Markup veranschaulicht, wie die Steuerelemente **SharePoint:CssLink** und **SharePoint:CssRegistration** verwenden.</span><span class="sxs-lookup"><span data-stu-id="028cc-p115">If you need to include a cascading style sheet (CSS) file, you need to use the **SharePoint:CssLink** and **SharePoint:CssRegistration** controls. These controls have been updated to work in both MDS and non-MDS mode. The following markup shows how to use the **SharePoint:CssLink** and **SharePoint:CssRegistration** controls.</span></span>
  
    
    



```HTML

<SharePoint:CssLink runat="server" Version="15"/>
<SharePoint:CssRegistration Name="my_stylesheet.css" runat="server" />
```


> <span data-ttu-id="028cc-183">**Vorsicht:** Es ist nur ein **SharePoint:CssLink**-Steuerelement pro Seite erlaubt.</span><span class="sxs-lookup"><span data-stu-id="028cc-183">**Caution:** You can have only one **SharePoint:CssLink** control per page.</span></span> <span data-ttu-id="028cc-184">Im MDS-Modus erhalten Sie eine Fehlermeldung, wenn Sie über mehr als ein **SharePoint:CssLink**-Steuerelement auf einer Seite verfügen.</span><span class="sxs-lookup"><span data-stu-id="028cc-184">In MDS mode, you get an error if you have more than one **SharePoint:CssLink** control in a page.</span></span> <span data-ttu-id="028cc-185">Das Einfügen einer CSS-Datei mit einem HTML-Stilelement wird im MDS-Modus nicht unterstützt, da die Serverlogik die Datei nicht als erforderliche Ressource identifizieren kann, wenn die Antwort gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="028cc-185">Caution Including a JavaScript file using the HTML script tag is not supported in MDS mode, because the server logic cannot identify the file as a required resource when the response is rendered.</span></span>
  
    
    

<span data-ttu-id="028cc-p117">Wenn Sie eine JavaScript-Datei einfügen möchten, verwenden Sie das **SharePoint:ScriptLink**-Steuerelement. Das folgende Markup zeigt, wie Sie das **SharePoint:ScriptLink**-Steuerelement verwenden.</span><span class="sxs-lookup"><span data-stu-id="028cc-p117">To include a JavaScript file, use the **SharePoint:ScriptLink** control. The following markup shows how to use the **SharePoint:ScriptLink** control.</span></span>
  
    
    



```HTML

<SharePoint:ScriptLink language="javascript" name="my_javascriptfile.js" runat="server" />
```


> <span data-ttu-id="028cc-188">**Vorsicht:** Das Einfügen einer JavaScript-Datei mit einem HTML-Skript-Tag wird im MDS-Modus nicht unterstützt, da die Serverlogik die Datei nicht als erforderliche Ressource identifizieren kann, wenn die Antwort gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="028cc-188">**Caution** Including a JavaScript file using the HTML script tag is not supported in MDS mode, because the server logic cannot identify the file as a required resource when the response is rendered.</span></span> 
  
    
    

<span data-ttu-id="028cc-p118">Zum Rendern von Title-Elements innerhalb des Head-Elements auf der Seite verwenden wir eine spezielle Muster mithilfe des **SharePoint:PageTitle** -Steuerelements. Das folgende Markup veranschaulicht, wie das **SharePoint:PageTitle** -Steuerelement verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="028cc-p118">To render the title element inside the head element in the page, we use a special pattern using the **SharePoint:PageTitle** control. The following markup shows how to use the **SharePoint:PageTitle** control.</span></span>
  
    
    



```HTML
<SharePoint:PageTitle runat="server">
    <asp:ContentPlaceHolder id="PlaceHolderPageTitle" runat="server" />
</SharePoint:PageTitle>

```


> <span data-ttu-id="028cc-191">**Hinweis:** Jede einzelne Seite muss den Titel durch Bereitstellen eines Ersatzes für das **Asp:ContentPlaceHolder**-Steuerelement innerhalb des **SharePoint:PageTitle** -Steuerelements überschreiben.</span><span class="sxs-lookup"><span data-stu-id="028cc-191">**Note** Each individual page must override the title by providing a replacement for the **asp:ContentPlaceHolder** control inside the **SharePoint:PageTitle** control.</span></span>
  
    
    


### <a name="aspnet-pages"></a><span data-ttu-id="028cc-192">ASP.NET-Seiten</span><span class="sxs-lookup"><span data-stu-id="028cc-192">ASP.NET pages</span></span>

<span data-ttu-id="028cc-193">Ein JavaScript oder eine CSS-Datei aufnehmen möchten, verwenden Sie die gleichen **SharePoint:ScriptLink** und **SharePoint:CssLink** Steuerelemente, die im vorherigen Abschnitt beschrieben.</span><span class="sxs-lookup"><span data-stu-id="028cc-193">To include a JavaScript or CSS file, use the same **SharePoint:ScriptLink** and **SharePoint:CssLink** controls described in the previous section.</span></span>
  
    
    
<span data-ttu-id="028cc-p119">In früheren Versionen von SharePoint schreibt einige Seiten die Inhalte mithilfe der **Response.Output** -Eigenschaft. Wenn Sie MDS verwenden, ist dies nicht mehr zulässig. Sie müssen die Aufrufe von **Response.Output** verwendet eine neue API zu ändern. Die folgende Tabelle enthält APIs, die häufig verwendet werden in SharePoint-Seiten und der neuen MDS-kompatibles-API.</span><span class="sxs-lookup"><span data-stu-id="028cc-p119">In previous versions of SharePoint, some pages write content by using the **Response.Output** property. If you are using MDS, this is no longer allowed. You have to change the calls to **Response.Output** to use a new API. The following table shows APIs that are commonly used in SharePoint pages and the new MDS-complaint API.</span></span>
  
    
    

<span data-ttu-id="028cc-198">**Tabelle 3. Häufig verwendete APIs und die zugehörigen MDS-kompatible Alternativen**</span><span class="sxs-lookup"><span data-stu-id="028cc-198">**Table 3. Commonly used APIs and their MDS-compliant alternatives**</span></span>


|<span data-ttu-id="028cc-199">**Häufig verwendete API**</span><span class="sxs-lookup"><span data-stu-id="028cc-199">**Commonly used API**</span></span>|<span data-ttu-id="028cc-200">**MDS-kompatible alternative**</span><span class="sxs-lookup"><span data-stu-id="028cc-200">**MDS-compliant alternative**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="028cc-201">NoEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-201">NoEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.NoEncode.aspx) <br/> | [<span data-ttu-id="028cc-202">WriteNoEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-202">WriteNoEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteNoEncode.aspx) <br/> |
| [<span data-ttu-id="028cc-203">HtmlEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-203">HtmlEncode</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.HtmlEncode.aspx) <br/> | [<span data-ttu-id="028cc-204">WriteHtmlEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-204">WriteHtmlEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncode.aspx) <br/> |
| [<span data-ttu-id="028cc-205">EcmaScriptStringLiteralEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-205">EcmaScriptStringLiteralEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.EcmaScriptStringLiteralEncode.aspx) <br/> | [<span data-ttu-id="028cc-206">WriteEcmaScriptStringLiteralEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-206">WriteEcmaScriptStringLiteralEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteEcmaScriptStringLiteralEncode.aspx) <br/> |
| [<span data-ttu-id="028cc-207">HtmlEncodeAllowSimpleTextFormatting()</span><span class="sxs-lookup"><span data-stu-id="028cc-207">HtmlEncodeAllowSimpleTextFormatting()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.HtmlEncodeAllowSimpleTextFormatting.aspx) <br/> | [<span data-ttu-id="028cc-208">WriteHtmlEncodeAllowSimpleTextFormatting()</span><span class="sxs-lookup"><span data-stu-id="028cc-208">WriteHtmlEncodeAllowSimpleTextFormatting()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlEncodeAllowSimpleTextFormatting.aspx) <br/> |
| [<span data-ttu-id="028cc-209">HtmlUrlAttributeEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-209">HtmlUrlAttributeEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.HtmlUrlAttributeEncode.aspx) <br/> | [<span data-ttu-id="028cc-210">WriteHtmlUrlAttributeEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-210">WriteHtmlUrlAttributeEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteHtmlUrlAttributeEncode.aspx) <br/> |
| [<span data-ttu-id="028cc-211">UrlKeyValueEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-211">UrlKeyValueEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.UrlKeyValueEncode.aspx) <br/> | [<span data-ttu-id="028cc-212">WriteUrlKeyValueEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-212">WriteUrlKeyValueEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlKeyValueEncode.aspx) <br/> |
| [<span data-ttu-id="028cc-213">UrlPathEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-213">UrlPathEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.UrlPathEncode.aspx) <br/> | [<span data-ttu-id="028cc-214">WriteUrlPathEncode()</span><span class="sxs-lookup"><span data-stu-id="028cc-214">WriteUrlPathEncode()</span></span>](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPHttpUtility.WriteUrlPathEncode.aspx) <br/> |
   
<span data-ttu-id="028cc-p120">Wenn eine Seite, Steuerelement oder Webpart, deren Ausgabe der **Response.Output** -Eigenschaft anweist, kann dies MDS Failback. Wenn MDS wieder ein Fehler auftritt, führt er eine vollständige Navigation auf die angeforderte Seite. Mithilfe der **DeltaPage ._shipRender** -Eigenschaft während des Debuggens Serverkomponente finden Sie das betreffende Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="028cc-p120">If a page, control, or Web Part directs its output to the **Response.Output** property, it causes MDS to fail back. When MDS fails back, it performs a full navigation to the requested page. You can find the offending control by using the **DeltaPage ._shipRender** property while debugging the server component.</span></span>
  
    
    
<span data-ttu-id="028cc-p121">Sie sollten mit Steuerelementen **SharePoint:ScriptBlock** HTML Inline Skriptelemente ersetzen. Die folgende Tabelle zeigt eine HTML-Inline Script-Element und ein **SharePoint:ScriptBlock** -Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="028cc-p121">You should replace HTML inline script elements with **SharePoint:ScriptBlock** controls. The following table shows an HTML inline script element and a **SharePoint:ScriptBlock** control.</span></span>
  
    
    

<span data-ttu-id="028cc-220">**In Tabelle 4. HTML Inline Script-Element und dessen MDS-kompatible alternative**</span><span class="sxs-lookup"><span data-stu-id="028cc-220">**Table 4. HTML inline script element and its MDS-compliant alternative**</span></span>


|<span data-ttu-id="028cc-221">**HTML Inline Script-element**</span><span class="sxs-lookup"><span data-stu-id="028cc-221">**HTML inline script element**</span></span>|<span data-ttu-id="028cc-222">**MDS-kompatible alternative**</span><span class="sxs-lookup"><span data-stu-id="028cc-222">**MDS-compliant alternative**</span></span>|
|:-----|:-----|
|`<script type="text/javascript">`<br/>&nbsp;&nbsp;&nbsp;`// Your JavaScript code goes here.`<br/>`</script>`|`<SharePoint:ScriptBlock runat="server">`<br/>&nbsp;&nbsp;&nbsp;`// Your JavaScript code goes here.`<br/>`</SharePoint:ScriptBlock>`|
   
<span data-ttu-id="028cc-p122">Die Einführung der **SharePoint:ScriptBlock** auf der Seite kann den Bereich der Variablen auf der Seite ändern. Manchmal ist es erforderlich, verschieben die Deklaration von Variablen von `<% %>` zu `<script runat="server"> <script>`. Laden Sie die Seite im Browser nach Updates ausführen, um dies zu testen.</span><span class="sxs-lookup"><span data-stu-id="028cc-p122">The introduction of the **SharePoint:ScriptBlock** in the page can change the scope of variables in page. Sometimes it is necessary to move the declaration of variables from `<% %>` to `<script runat="server"> <script>`. To test this, load the page in the browser after you perform updates.</span></span>
  
    
    

> <span data-ttu-id="028cc-226"> **Hinweis:** Die MDS-Infrastruktur unterstützt VBScript nicht, da es nicht als Skript in ASP.NET erfasst werden kann.</span><span class="sxs-lookup"><span data-stu-id="028cc-226">**Note** The MDS infrastructure does not support VBScript, because it cannot be registered as a script in ASP.NET. Scripts have to be converted to JavaScript.</span></span> <span data-ttu-id="028cc-227">Skripts müssen in JavaScript konvertiert werden.</span><span class="sxs-lookup"><span data-stu-id="028cc-227">Scripts have to be converted to JavaScript.</span></span> 
  
    
    

<span data-ttu-id="028cc-p124">Links in ASP.NET Seiten müssen aktualisiert werden, um **SPUpdatePage** Typ zu verwenden. Tabelle 5 zeigt Hyperlinks in ASP.NET Seiten und die gleiche Links mit **SPUpdatePage** Typ aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="028cc-p124">HyperLinks in ASP.NET pages must be updated to use **SPUpdatePage** type. Table 5 shows hyperlinks in ASP.NET pages and the same links updated by using **SPUpdatePage** type.</span></span>
  
    
    

<span data-ttu-id="028cc-230">**Tabelle 5. Hyperlink in ASP.NET und dessen MDS-kompatible alternative**</span><span class="sxs-lookup"><span data-stu-id="028cc-230">**Table 5. Hyperlink in ASP.NET and its MDS-compliant alternative**</span></span>


|<span data-ttu-id="028cc-231">**Hyperlink in ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="028cc-231">**Hyperlink in ASP.NET**</span></span>|<span data-ttu-id="028cc-232">**MDS-kompatible alternative**</span><span class="sxs-lookup"><span data-stu-id="028cc-232">**MDS-compliant alternative**</span></span>|
|:-----|:-----|
|`<a`<br/>&nbsp;&nbsp;&nbsp;`id=<%_STSWriteHTML("viewlist" + spList.BaseTemplate.ToString());%>`<br/>&nbsp;&nbsp;&nbsp;`href=<%_STSWriteURL(listViewUrl);%>`<br/>`>`|`<a`<br/>&nbsp;&nbsp;&nbsp;`id=<%_STSWriteHTML("viewlist" + spList.BaseTemplate.ToString());%>`<br/>&nbsp;&nbsp;&nbsp;`href=<%_STSWriteURL(listViewUrl);%>`<br/>&nbsp;&nbsp;&nbsp;`onclick="if (typeof(SPUpdatePage) !== 'undefined') return SPUpdatePage(this.href);"`<br/>`>`|
   

### <a name="custom-master-pages-for-errors"></a><span data-ttu-id="028cc-233">Benutzerdefinierte Masterseiten für Fehler</span><span class="sxs-lookup"><span data-stu-id="028cc-233">Custom master pages for errors</span></span>

<span data-ttu-id="028cc-p125">Auch wenn Sie eine benutzerdefinierte Gestaltungsvorlage für die Fehler verwenden, können Sie Fehlermeldungen in MDS-Modus anzeigen. Um eine benutzerdefinierte Gestaltungsvorlage für Fehler im MDS-Modus verwenden, müssen Sie ein **AjaxDelta** in der Gestaltungsvorlage Fehler definieren, die die **Id** -Eigenschaft auf die Zeichenfolge **"DeltaPlaceHolderMain"** festgelegt wurde. Der Inhalt der Fehlermeldung muss in der **AjaxDelta** gerendert werden. Wenn die Fehlerseite vom Server an den Browser zurückgegeben wird, wird der Browser identifiziert dies als der Hauptinhalt angezeigt und zeigt es dem Benutzer.</span><span class="sxs-lookup"><span data-stu-id="028cc-p125">You can display error messages in MDS mode, even when you are using a custom master page for errors. To use a custom master page for errors in MDS mode, you must define an **AjaxDelta** in the error master page that has the **id** property set to the string **"DeltaPlaceHolderMain"**. The content of the error message must be rendered into the **AjaxDelta**. When the error page is returned to the browser from the server, the browser identifies this as the main content to display and shows it to the user.</span></span>
  
    
    
<span data-ttu-id="028cc-p126">Obwohl die Masterseite für die Fehlerseite und die Masterseite für **start.aspx** sind kein explizite Übereinstimmung, kann den Browser zu erkennen, dass ein Fehler aufgetreten ist. Der Browser ermöglicht MDS den entsprechenden Fehlermeldungen Nachrichteninhalt innerhalb der vorhandenen Masterseite verwenden, um eine konsistente und reibungslose benutzererfahrung verwalten.</span><span class="sxs-lookup"><span data-stu-id="028cc-p126">Although the master page for the error page and the master page for **start.aspx** are not an explicit match, the browser can detect that an error has occurred. The browser allows MDS to use the relevant error message content within the existing master page in order to maintain a consistent and smooth user experience.</span></span>
  
    
    

### <a name="javascript-files"></a><span data-ttu-id="028cc-240">JavaScript-Dateien</span><span class="sxs-lookup"><span data-stu-id="028cc-240">JavaScript files</span></span>

<span data-ttu-id="028cc-p127">JavaScript Dateien sollte nur Deklarationen enthalten. Es gibt dennoch viele legacy-Skripts, die globalen Variablen wie enthalten. Globale Variablen müssen erneut initialisiert werden, wenn eine neue Seite im Modus MDS gerendert wird. Sie können die **ExecuteAndRegisterBeginEndFunctions** verwenden, um globalen Variablen zu initialisieren. Im folgenden Codebeispiel wird veranschaulicht, wie die **ExecuteAndRegisterBeginEndFunctions**verwenden.</span><span class="sxs-lookup"><span data-stu-id="028cc-p127">JavaScript files should include only function declarations. Nonetheless, there are many legacy scripts that contain global variable initializations. Global variables need to be reinitialized when a new page is rendered in MDS mode. You can use the **ExecuteAndRegisterBeginEndFunctions** to initialize global variables. The following code example shows how to use the **ExecuteAndRegisterBeginEndFunctions**.</span></span>
  
    
    

```

function ExecuteAndRegisterBeginEndFunctions(tag, beginFunc, endFunc, loadFunc)

```

<span data-ttu-id="028cc-246">Die **ExecuteAndRegisterBeginEndFunctions** hat die folgenden Parameter:</span><span class="sxs-lookup"><span data-stu-id="028cc-246">The **ExecuteAndRegisterBeginEndFunctions** has the following parameters:</span></span>
  
    
    

-  <span data-ttu-id="028cc-247">_tag_: der Name der Datei, die die Rückrufe; registriert Es wird nur zu Debuggingzwecken verwendet.</span><span class="sxs-lookup"><span data-stu-id="028cc-247">_tag_: The name of the file that registers the callbacks; it is used only for debugging purposes.</span></span>
    
  
-  <span data-ttu-id="028cc-248">_beginFunc_: eine Funktion, die aufgerufen wird, bevor Sie das Seite Delta anfordern.</span><span class="sxs-lookup"><span data-stu-id="028cc-248">_beginFunc_: A function that is called before you request the page delta.</span></span>
    
  
-  <span data-ttu-id="028cc-249">_endFunc_: eine Funktion, die aufgerufen wird, nachdem Sie das Delta abgerufen, jedoch bevor der HTML- und JavaScript für die neue Seite angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="028cc-249">_endFunc_: A function that is called after you retrieve the delta, but before the HTML and JavaScript for the new page are applied.</span></span>
    
  
-  <span data-ttu-id="028cc-250">_loadFunc_: eine Funktion, die nach der HTML- und JavaScript aufgerufen wird, für die neue Seite angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="028cc-250">_loadFunc_: A function that is called after the HTML and JavaScript for the new page is applied.</span></span>
    
  

### <a name="controls-and-web-parts"></a><span data-ttu-id="028cc-251">Steuerelemente und Webparts</span><span class="sxs-lookup"><span data-stu-id="028cc-251">Controls and Web Parts</span></span>

<span data-ttu-id="028cc-p128">Um MDS verwenden, müssen Steuerelemente und Webparts Seitenressourcen registrieren mithilfe des **SPPageContentManager** -Objekts. Die am häufigsten registrierten Ressourcen mit **SPPageContentManager** sind JavaScript Snippets (Funktionen oder JSON-Variablen) und ausgeblendeten Feldern. Die folgende Tabelle zeigt gängiger Muster für das Einfügen von ausgeblendeten Felder und JavaScript Codeausschnitte und wie Sie die gleichen mithilfe des **SPPageContentManager** -Objekts.</span><span class="sxs-lookup"><span data-stu-id="028cc-p128">To use MDS, controls and Web Parts have to register page resources by using the **SPPageContentManager** object. The most frequently registered resources using **SPPageContentManager** are JavaScript snippets (functions or JSON variables) and hidden fields. The following table shows common patterns for inserting hidden fields and JavaScript snippets, and how to do the same by using the **SPPageContentManager** object.</span></span>
  
    
    

<span data-ttu-id="028cc-255">**Tabelle 6. Allgemeine Methoden für das Rendering des Inhalts und die zugehörigen MDS-kompatible Alternativen**</span><span class="sxs-lookup"><span data-stu-id="028cc-255">**Table 6. Common practices for rendering content and their MDS-compliant alternatives**</span></span>


|<span data-ttu-id="028cc-256">**Üblich zum Rendern von Inhalt**</span><span class="sxs-lookup"><span data-stu-id="028cc-256">**Common practice for rendering content**</span></span>|<span data-ttu-id="028cc-257">**MDS-kompatible Alternative**</span><span class="sxs-lookup"><span data-stu-id="028cc-257">**MDS-compliant alternative**</span></span>|
|:-----|:-----|
|`output.Write("<input type=\\"hidden\\" name=\\"");`<br/>`output.Write(SPHttpUtility.NoEncode("HiddenField));`<br/>`output.Write("\\" value=\\"");`<br/>`output.Write(DigestValue);`<br/>`output.Write("\\" />");`|`SPPageContentManager.RegisterHiddenField(this, "HiddenField", DigestValue);`|
|`Page.ClientScript.RegisterClientScriptBlock(typeof(MyType), "MyKey", "var myvar=1", true);`|`SPPageContentManager.RegisterClientScriptBlock(this, typeof(MyType), "MyKey", "var myvar=1");`|
   

> <span data-ttu-id="028cc-258">**Hinweis:** Die Funktionen **RegisterHiddenField** und **RegisterClientScriptBlock** im **SPPageContentManager**-Objekt erwarten, dass sich ein Objekt vom Typ **Steuerelement** oder **Seite** im ersten Parameter befindet.</span><span class="sxs-lookup"><span data-stu-id="028cc-258">**Note** The **RegisterHiddenField** and **RegisterClientScriptBlock** functions in the **SPPageContentManager** object expect an object of type **Control** or **Page** in the first parameter.</span></span>
  
    
    

<span data-ttu-id="028cc-p129">Das Modul MDS verwendet den ersten Parameter, um die Skripts filtern. Hier werden die Regeln für die Filterung beim Rendern einer Seite im MDS Deltamodus:</span><span class="sxs-lookup"><span data-stu-id="028cc-p129">The MDS engine uses the first parameter to filter the scripts. Here are the rules for filtering when a page is rendered in MDS delta mode:</span></span>
  
    
    

- <span data-ttu-id="028cc-261">Wenn das erste Argument vom Typ **Seite** ist, werden die Skripts im Browser ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="028cc-261">If the first argument is of type **Page**, the scripts will execute in the browser.</span></span>
    
  
- <span data-ttu-id="028cc-262">Wenn das erste Argument nicht vom Typ **Seite ist** und das Steuerelement unter einem **SharePoint:AsyncDelta fällt**, werden im Browser die Skripts ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="028cc-262">If the first argument is not of type **Page** and the control falls under a **SharePoint:AsyncDelta**, the scripts will execute in the browser.</span></span>
    
  
- <span data-ttu-id="028cc-263">Wenn das erste Argument ein Webpart ist, werden die Skripts im Browser ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="028cc-263">If the first argument is a Web Part, the scripts will execute in the browser.</span></span>
    
  
<span data-ttu-id="028cc-p130">Viele APIs in früheren Versionen von SharePoint hat das aktuelle Steuerelement als ein Argument nicht bereitgestellt. Das public-Objektmodell in SharePoint bietet eine alternative Methode, um die Ressourcen zu registrieren. Die Methoden, die das aktuelle Steuerelement als Argument keine bereitstellen sind weiterhin in der API für Abwärtskompatibilität.</span><span class="sxs-lookup"><span data-stu-id="028cc-p130">Many APIs in previous versions of SharePoint did not provide the current control as an argument. The public object model in SharePoint was designed to provide an alternate method to register the resources. The methods that do not provide the current control as an argument are still in the API for backward compatibility.</span></span>
  
    
    
<span data-ttu-id="028cc-p131">Sie können zwischen zwei Seiten mithilfe einer neuen Funktion mit dem Namen **SPUpdatePage**navigieren. Wenn ein Steuerelement oder Webpart im MDS Deltamodus gerendert wird, müssen die Steuerelemente **HyperLink** fügen Sie den Ereignishandler **onclick** und **SPUpdatePage**aufrufen.</span><span class="sxs-lookup"><span data-stu-id="028cc-p131">You can navigate between two pages by using a new function named **SPUpdatePage**. When a control or Web Part is rendered in MDS delta mode, the **HyperLink** controls must add the **onclick** handler and call **SPUpdatePage**.</span></span>
  
    
    
<span data-ttu-id="028cc-p132">Aktualisieren Sie die XSLT von Webparts verwendet werden, da alle Ressourcen hinzugefügt werden müssen, mithilfe des **SPPageContentManager** -Objekts um zu machen MDS-kompatibel. Sie können die XSLT JavaScript Snippets mithilfe der Methods **RegisterScriptLink** und **RegisterScriptBlock** des **SPPageContentManager** -Objekts hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="028cc-p132">You must update the XSLT used by Web Parts because all the resources must be added by using the **SPPageContentManager** object to make them MDS-compliant. You can add JavaScript snippets to the XSLT by using the **RegisterScriptLink** and **RegisterScriptBlock** methods of the **SPPageContentManager** object.</span></span>
  
    
    

## <a name="optimize-page-downloads"></a><span data-ttu-id="028cc-271">Optimieren der Seite downloads</span><span class="sxs-lookup"><span data-stu-id="028cc-271">Optimize page downloads</span></span>
<span data-ttu-id="028cc-272"><a name="MDS"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-272"></span></span>

<span data-ttu-id="028cc-p133">Wenn Sie die Zusammensetzung des einer Seite verstanden haben, können Sie verschiedene Methoden verwenden, um den Download für diese Seite zu optimieren. Im Allgemeinen ist das Ziel, um die Anzahl von Roundtrips zwischen Client und Server-Computern zu minimieren und die Datenmenge zu reduzieren, die über das Netzwerk wechselt. Die Anleitung in diesem Artikel enthält Empfehlungen, die Sie im Allgemeinen gibt es für eine Vielzahl von verschiedenen Implementierungen von SharePoint anwenden können.</span><span class="sxs-lookup"><span data-stu-id="028cc-p133">Once you understand the composition of a page, you can use different methods to optimize the download experience for that page. In general, the goal is to minimize the number of round trips between client and server computers and to reduce the amount of data that goes over the network. The guidance in this article includes recommendations that you can apply broadly to a variety of different implementations of SharePoint.</span></span>
  
    
    
<span data-ttu-id="028cc-276">In Tabelle 7 sind Ladezeiten, die veranschaulichen, den Unterschied zwischen dem ersten Beispiel Zweitens und nachfolgenden Seite geladen wird.</span><span class="sxs-lookup"><span data-stu-id="028cc-276">Table 7 shows example loading times that illustrate the difference between the first, second, and subsequent page loads.</span></span>
  
    
    

<span data-ttu-id="028cc-277">**Tabelle 7. Wie oft Laden der Seite**</span><span class="sxs-lookup"><span data-stu-id="028cc-277">**Table 7. Page loading times**</span></span>

|||
|:-----|:-----|
|<span data-ttu-id="028cc-278">Laden der ersten Seite</span><span class="sxs-lookup"><span data-stu-id="028cc-278">First page load</span></span>  <br/> |<span data-ttu-id="028cc-279">3-4 Sekunden</span><span class="sxs-lookup"><span data-stu-id="028cc-279">3-4 seconds</span></span>  <br/> |
|<span data-ttu-id="028cc-280">Laden der zweiten Seite</span><span class="sxs-lookup"><span data-stu-id="028cc-280">Second page load</span></span>  <br/> |<span data-ttu-id="028cc-281">15 Sekunden</span><span class="sxs-lookup"><span data-stu-id="028cc-281">1.5 seconds</span></span>  <br/> |
|<span data-ttu-id="028cc-282">Die Seite anschließend geladen</span><span class="sxs-lookup"><span data-stu-id="028cc-282">Subsequent page loads</span></span>  <br/> |<span data-ttu-id="028cc-283">1 Sekunde</span><span class="sxs-lookup"><span data-stu-id="028cc-283">1 second</span></span>  <br/> |
   

> <span data-ttu-id="028cc-284">**Hinweis:** Die Ladezeiten können in Ihrem Szenario unterschiedlich sein.</span><span class="sxs-lookup"><span data-stu-id="028cc-284">**Note:** Loading times might be different in your particular scenario.</span></span> <span data-ttu-id="028cc-285">Die Ladezeiten werden von vielen Faktoren beeinflusst, einschließlich, aber nicht beschränkt auf die Seitengröße, die Latenz und die Serverlast.</span><span class="sxs-lookup"><span data-stu-id="028cc-285">Note Loading times might be different in your particular scenario. Loading times are affected by many variables, including, but not limited to, page size, latency, and server load.</span></span> 
  
    
    

<span data-ttu-id="028cc-p135">Sie sollten seitenoptimierungstechniken in zwei Kategorien unterteilt: die erste Seite Anforderung und nachfolgende Seitenanforderungen. Optimierungen für die erste Seitenanforderung (Seite des Ladens 1 oder PLT1) sind diese Arten von Optimierungen, die eine effektive erstmals die Seite angefordert wird, jedoch nicht unbedingt nachfolgende Seitenanforderungen beeinträchtigt werden. Im folgenden sind einige Optimierungen für PLT1:</span><span class="sxs-lookup"><span data-stu-id="028cc-p135">You should categorize page optimization techniques into one of two categories: first page request and subsequent page requests. Optimizations for the first page request (page load time 1 or PLT1) are those kinds of optimizations that are effective the first time the page is requested, but that don't necessarily affect subsequent page requests. The following are some optimizations for PLT1:</span></span>
  
    
    

- <span data-ttu-id="028cc-289">Optimieren Sie HTML-Markup.</span><span class="sxs-lookup"><span data-stu-id="028cc-289">Optimize HTML markup.</span></span>
    
  
- <span data-ttu-id="028cc-p136">Verwenden Sie konsolidierten Bilder und Dateien. Kombinieren Sie beispielsweise mehrere CSS-Dateien in eine. Kombinieren Sie Bilder in einem Bildstreifen oder Cluster.</span><span class="sxs-lookup"><span data-stu-id="028cc-p136">Use consolidated images and files; for example, combine multiple CSS files into one. Combine images into an image strip or cluster.</span></span>
    
  
- <span data-ttu-id="028cc-p137">Verwenden Sie Komprimierungstechniken (Crunch) Techniken. Weitere Informationen finden Sie unter  [Komprimieren Sie (crunchen) JavaScript und CSS-Dateien](optimize-page-performance-in-sharepoint.md#OptimizingPagePerformance_Crunch).</span><span class="sxs-lookup"><span data-stu-id="028cc-p137">Use compression (crunch) techniques. For more information, see  [Compress (crunch) JavaScript and CSS files](optimize-page-performance-in-sharepoint.md#OptimizingPagePerformance_Crunch).</span></span>
    
  
- <span data-ttu-id="028cc-294">Stellen Sie sicher, dass Sie die Produktionsversion üblichen JavaScript Bibliotheken wie jQuery, anstatt die Debugversionen verweisen.</span><span class="sxs-lookup"><span data-stu-id="028cc-294">Verify that you are referencing the production version of common JavaScript libraries, such as jQuery, instead of the debug versions.</span></span>
    
  
- <span data-ttu-id="028cc-p138">Erwägen Sie eine bekannte Content Delivery Network (CDN) wie die  [Microsoft Ajax Content Delivery Network](http://www.asp.net/ajaxlibrary/cdn.ashx). Auf den Seiten erforderlichen Dateien möglicherweise bereits vom Clientbrowser zwischengespeichert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="028cc-p138">Consider using a well-known content delivery network (CDN) such as the  [Microsoft Ajax Content Delivery Network](http://www.asp.net/ajaxlibrary/cdn.ashx). The files required in your pages may already be cached by the client browser.</span></span>
    
  
<span data-ttu-id="028cc-p139">Optimierungen für nachfolgende Seitenanforderungen sind die, die die Benutzeroberfläche für eine Auslastung der nachfolgenden Seite verbessert werden kann. Der Schlüssel ist, die Sie benötigen, um Verlust in Funktionalität für die Verstärkung erreicht auszugleichen. Wenn Gewinn nur beim ersten realisiert ist ein Benutzer eine Website besucht, die Optimierung möglicherweise nicht lohnt des Verlust an Funktionalität.</span><span class="sxs-lookup"><span data-stu-id="028cc-p139">Optimizations for subsequent page requests are those that can improve the user experience for a subsequent page load. The key is that you need to balance loss in functionality against the gain achieved. If gain is only realized the first time a user hits a site, the optimization might not be worth the loss in functionality.</span></span>
  
    
    

## <a name="compress-crunch-javascript-and-css-files"></a><span data-ttu-id="028cc-300">Komprimieren Sie (crunchen) JavaScript und CSS-Dateien</span><span class="sxs-lookup"><span data-stu-id="028cc-300">Compress (crunch) JavaScript and CSS files</span></span>
<span data-ttu-id="028cc-301"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-301"></span></span>

<span data-ttu-id="028cc-p140">Dateien, die JavaScript und Formatvorlagen enthalten möglicherweise stark verkleinert werden durch Entfernen von Leerzeichen, Formatvorlage Vererbung und Wiederverwendung von Code. Einige Bibliotheken sind in regulären (Debug) und komprimierten Versionen (crunched). Sie können eine Vielzahl von Tools zum Automatisieren der Datei crunching über eine Suche im Internet suchen.</span><span class="sxs-lookup"><span data-stu-id="028cc-p140">Files that contain JavaScript and styles may be significantly reduced in size by removing whitespaces, style inheritance, and code reuse. Some libraries come in both regular (debug) and compressed (crunched) versions. You can find a variety of tools to automate file crunching by searching the Internet.</span></span>
  
    
    
<span data-ttu-id="028cc-p141">Stellen Sie sicher, dass die komprimierten Versionen in Produktionsservern bereitgestellt werden. Dieses Beispiel zeigt, wie eine CSS-Datei in Größe über einige relativ einfach Umschreiben von Adressen reduziert werden kann.</span><span class="sxs-lookup"><span data-stu-id="028cc-p141">Verify that the compressed versions are deployed to production servers. This example shows how a CSS file can be reduced in size through some relatively simple rewriting.</span></span>
  
    
    



```
.article-ByLine  {
  font-family: Tahoma,sans-serif; 
  font-size: 9.5pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: normal; 
  color: #000000
}
.article-Caption { 
  font-family: Tahoma,sans-serif; 
  font-size: 8pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: normal; 
  color: #000000
}
.article-Headline { 
  font-family: Tahoma,sans-serif; 
  font-size: 14pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: bold; 
  color: #000000
}
.article-SubHead  { 
  font-family: Tahoma, sans-serif; 
  font-size: 11pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: normal; 
  color: #000000
}
.article-Text {
  font-family: Tahoma, sans-serif; 
  font-size: 10pt; 
  font-style: normal; 
  line-height: normal; 
  font-weight: normal; 
  color: #000000
}

```

<span data-ttu-id="028cc-p142">In der Regel finden Sie Verfahren zum Erreichen der gleichen Stil und verringern Sie die Größe der Dateien von effizient umschreiben CSS-Dateien. Im folgenden Beispiel wird veranschaulicht, wie auf die vorherige Größe CSS optimieren, indem Sie die Formatvorlagen von einem übergeordneten Element erben.</span><span class="sxs-lookup"><span data-stu-id="028cc-p142">You can usually find ways to achieve the same styling and reduce the size of your files by efficiently rewriting your CSS files. The following example shows how to optimize the previous CSS size by inheriting the styles from a parent element.</span></span>
  
    
    



```

BODY {font:100% Tahoma,sans-serif}
.art-By {font: 79%}
.art-Cap {font: 67%}
.art-Head {font: bold 117%}
.art-Sub {font: 92%}
.art-Txt {font: 83%}
```

<span data-ttu-id="028cc-309">Die erste Version des CSS ist 783 Zeichen lang sein darf, und die zweite beträgt 140 Zeichen lang sein darf.</span><span class="sxs-lookup"><span data-stu-id="028cc-309">The first version of the CSS is 783 characters long, and the second is 140 characters long.</span></span>
  
    
    

## <a name="entity-tags"></a><span data-ttu-id="028cc-310">Entity-tags</span><span class="sxs-lookup"><span data-stu-id="028cc-310">Entity tags</span></span>
<span data-ttu-id="028cc-311"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-311"></span></span>

<span data-ttu-id="028cc-p143">Entitätstags (ETags) kann den Client Dateien unnötig erneut zu laden. ETags sollen Dateien anhand einer Zahl, die der Server generiert eindeutig zu identifizieren. In der Server-Clustern wird jeder Server eine unterschiedliche Anzahl erstellt. Beispielsweise ist ein Browser **Get** -Methode mit einem **If-Modified** -Header-Feld für eine Datei senden, die es in seinem Cache gefunden. Ist nur einen Server, die Datei wird wahrscheinlich übereinstimmen, und ein **304 Not-Modified** HTTP-Status wird gesendet. Aber, wenn der Benutzer auf eine große Serverfarm zugreift, wird es wahrscheinlich einen anderen Server mit einem anderen Entitätstag, verursacht diese Server zum Senden der Datei an den Browser erreicht.</span><span class="sxs-lookup"><span data-stu-id="028cc-p143">Entity tags (ETags) can cause the client to unnecessarily reload files. ETags are meant to uniquely identify files by using a number that the server generates. In clusters of servers, each server will create a different number. For example, a browser is sending a **Get** method with an **If-Modified** header field for a file that it found in its cache. If there is only one server, the file will probably match, and a **304 Not-Modified** http status will be sent. But, if the user is accessing a large server farm, it will probably hit a different server with a different entity tag, causing that server to send the file to the browser.</span></span>
  
    
    

## <a name="cache-settings"></a><span data-ttu-id="028cc-318">Cacheeinstellungen</span><span class="sxs-lookup"><span data-stu-id="028cc-318">Cache settings</span></span>
<span data-ttu-id="028cc-319"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-319"></span></span>

<span data-ttu-id="028cc-p144">Verwenden Sie Fiddler oder einem ähnlichen Tool wird überprüft, ob der Cache Anforderungen verarbeitet wird. Häufige Ursachen für Zwischenspeichern nicht verarbeiten Anforderungen umfassen:</span><span class="sxs-lookup"><span data-stu-id="028cc-p144">Use Fiddler or a similar tool to verify whether the cache is serving requests. Some common reasons caching not serving requests include:</span></span>
  
    
    

- <span data-ttu-id="028cc-322">Einen Datumswert Ablauf keine Ressourcen.</span><span class="sxs-lookup"><span data-stu-id="028cc-322">Resources do not have an expiration date value.</span></span>
    
  
- <span data-ttu-id="028cc-323">Die Abfragezeichenfolge ändert ständig.</span><span class="sxs-lookup"><span data-stu-id="028cc-323">The query string constantly changes.</span></span>
    
  
- <span data-ttu-id="028cc-324">Die Summe der **Max-Age** cachesteuerelement Richtlinie plus **last-modified** Header erzeugt ein Datum vor heute.</span><span class="sxs-lookup"><span data-stu-id="028cc-324">The sum of **max-age** cache-control directive plus **last-modified** header results in a date previous to today.</span></span>
    
  
- <span data-ttu-id="028cc-325">Die **Max-Age** -Eigenschaft unterstützt die Proxy-Server nicht.</span><span class="sxs-lookup"><span data-stu-id="028cc-325">The proxy servers do not support the **max-age** property.</span></span>
    
  
- <span data-ttu-id="028cc-p145">Der **Cache-Control-** Header hat den Wert **Nein-Cache**. Ein Wert von **privaten** speichert die Ressource nur für den Benutzer, der die Anforderung ausgibt.</span><span class="sxs-lookup"><span data-stu-id="028cc-p145">The **cache-control** header has a value of **no-cache**. A value of **private** caches the resource only for the user that issues the request.</span></span>
    
  

## <a name="number-and-size-of-images"></a><span data-ttu-id="028cc-328">Anzahl und Größe von Bildern</span><span class="sxs-lookup"><span data-stu-id="028cc-328">Number and size of images</span></span>
<span data-ttu-id="028cc-329"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-329"></span></span>

<span data-ttu-id="028cc-p146">Sie sollten die Anzahl der Bilder in Ihrer Website minimieren. Damit mit dieser Aufwand gewährleistet ist, können Sie mehrere Bilder in einer einzigen Datei einbetten und dann einzelne Bilder auf der Seite verweisen. Nicht nur Download Dateigröße verschlechtert, sondern weniger Dateien weniger Netzwerkverkehr führen. Es ist zum Erstellen von Seiten mithilfe dieses Verfahrens komplizierter, aber in Situationen, wo jedem Roundtrip und Dateigröße ankommt, kann es nachweisen, wertvolle Lösung zur Verbesserung von Leistung. Abbildung 3 zeigt ein Beispiel für eine einzelne Bilddatei, die mehrere Bilder enthält.</span><span class="sxs-lookup"><span data-stu-id="028cc-p146">You should minimize the number of images in your site. To help with that effort, you can embed multiple images in a single file and then reference individual images in your page. Not only will file download size decrease, but fewer files result in less network traffic. It is more complicated to author pages by using this technique, but in situations where every round trip and file size counts, it can prove to be valuable way to help improve performance. Figure 3 shows an example of a single image file that contains multiple images.</span></span>
  
    
    

<span data-ttu-id="028cc-335">**Abbildung 3. Einzelne Bilddatei an, die mehrere Bilder enthält**</span><span class="sxs-lookup"><span data-stu-id="028cc-335">**Figure 3. Single image file that contains multiple images**</span></span>

  
    
    

  
    
    
![Datei mit nur einem Bild, die mehrere Bilder enthält](../images/OptimizePage_Fig03_SingleImage.png)
  
    
    
<span data-ttu-id="028cc-337">Abbildung 4 zeigt, wie die Bilddatei später geändert wird, um als einzelne Bilder in einer Tabelle anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="028cc-337">Figure 4 shows how the image file is subsequently changed to display as individual pictures in a table.</span></span>
  
    
    

<span data-ttu-id="028cc-338">**Abbildung 4. Mehrere Bilder in einer Tabelle dargestellte**</span><span class="sxs-lookup"><span data-stu-id="028cc-338">**Figure 4. Multiple images displayed in a table**</span></span>

  
    
    

  
    
    
![Mehrere in einer Tabelle dargestellte Bilder](../images/OptimizePage_Fig04_ImageTable.png)
  
    
    
<span data-ttu-id="028cc-p147">Die Änderung dieser Bilder erfolgt komplett über Stylesheetklassen. Es wurden zwei primäre Klassen in **div**- und **img**-Elementen in jeder Tabellenzelle verwendet. Diese Klassen lauten wie folgt:</span><span class="sxs-lookup"><span data-stu-id="028cc-p147">Manipulation of the images was done entirely through style sheet classes. There were two primary classes used in **div** and **img** elements in each table cell. Those classes are as follows.</span></span>
  
    
    



```

BODY {font:100% Tahoma,sans-serif}
.art-By  {font: 79%}
.art-Cap {font: 67%}
.art-Head {font: bold 117%}
.art-Sub  {font: 92%}
.art-Txt {font: 83%}


.cluster { 
   height:50px; 
   position:relative; 
   width:50px; 
} 
.cluster img { 
   position:absolute; 
}
```

<span data-ttu-id="028cc-p148">Jedem Bild ist basierend auf dem Bezeichner (ID) für das Bild eine Klasse zugeordnet. Dieser Stil beschneidet das Bild und definiert ein Offset aus dem anfänglichen Bild im Cluster. Diese Klassen lauten wie folgt:</span><span class="sxs-lookup"><span data-stu-id="028cc-p148">Each image has a class associated with it based on the identifier (ID) for the image. That style clips the picture and defines an offset from the initial picture in the cluster. Those classes are as follows.</span></span>
  
    
    



```

#person {
   border:none; 
   clip:rect(0, 49, 49, 0); 
} 
#keys { 
   clip:rect(0, 99, 49, 50); 
   left:-50px; 
} 
#people { 
   clip: rect(0, 149, 49, 100); 
   left:-100px; 
} 
#lock { 
   clip:rect(0, 199, 49, 150); 
   left:-150px; 
} 
#phone { 
   clip:rect(0,249, 49, 200); 
   left:-200px; 
}
#question {
    clip: rect(0, 299, 49, 250);
    left: -250px;
}
```


## <a name="list-view-pages"></a><span data-ttu-id="028cc-346">Listenansichtsseiten</span><span class="sxs-lookup"><span data-stu-id="028cc-346">List view pages</span></span>
<span data-ttu-id="028cc-347"><a name="OptimizingPagePerformance_Crunch"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-347"></span></span>

<span data-ttu-id="028cc-p149">Microsoft hat funktioniert, um quantifizieren und Verbessern der Leistung der Liste Ansicht Seite Rendering Zeiten. Eine Seite mit der Listenansicht ist die AllItems.aspx-Seite, die von jedem Listen- und Bibliotheksdaten zum Durchsuchen von Inhalten aktivieren verwendet wird. Die Renderzeit dieser Seite kann weit basierend auf der Anzahl der Spalten, die in der Ansicht sichtbar sind und das Format der Spalten variieren. Beispielsweise können Optionen anzeigen und Aktivieren von Anwesenheitssymbole Renderzeit erheblich beeinträchtigen. Die Gruppierungsoption reduzierten wesentlich länger als die Gruppierungsoption erweiterte gerendert wurde, und beide wurden in allen langsamer als die Gruppierungsoption keine.</span><span class="sxs-lookup"><span data-stu-id="028cc-p149">Microsoft has worked to quantify and improve the performance of list view page rendering times. A list view page is the AllItems.aspx page that is used by each list and library to enable browsing of content. The rendering time of that page can vary widely based on the number of columns that are visible in the view and the format of the columns. For example, displaying options and enabling presence icons can greatly affect rendering time. The collapsed grouping option took significantly longer to render than the expanded grouping option, and both were slower than no grouping option at all.</span></span>
  
    
    
<span data-ttu-id="028cc-p150">Diese Art von Nuancen sind, warum es ist wichtig, überlegen Sie sich wie Ansichten in der Liste anzeigen, Seiten anzeigen, insbesondere über langsame Verbindungen erstellt werden. Bei der Verwendung von Listen, die eine große Datenmenge enthalten ist es wichtig, alle Ansichten, insbesondere die Standardansicht sorgfältig entwerfen. Im Allgemeinen können Sie die Zeit für das Rendering von Listenansichtsseiten beschleunigen, mithilfe der folgenden Empfehlungen:</span><span class="sxs-lookup"><span data-stu-id="028cc-p150">These sorts of nuances are why it is important to carefully consider how views are constructed in list view pages, especially over slow network connections. When working with lists that contain a lot of data, it is important to carefully design all views, especially the default view. In general, you can speed up the rendering time of list view pages by using the following recommendations:</span></span>
  
    
    

- <span data-ttu-id="028cc-356">Nur die unbedingt erforderlichen Spalten anzeigen.</span><span class="sxs-lookup"><span data-stu-id="028cc-356">Show only the strictly required columns.</span></span>
    
  
- <span data-ttu-id="028cc-357">Wenn möglich, schließen Sie Spalten aus, die Anwesenheitsinformationen enthalten.</span><span class="sxs-lookup"><span data-stu-id="028cc-357">If possible, exclude columns that include presence information.</span></span>
    
  
- <span data-ttu-id="028cc-358">Verwenden Sie einen Link zum Anzeigen der Elementdetails anstelle einer im Bearbeitungsmenü.</span><span class="sxs-lookup"><span data-stu-id="028cc-358">Use a link instead of an edit menu to view the item details.</span></span>
    
  
<span data-ttu-id="028cc-359">In der folgenden Tabelle sind die Anpassungen beschrieben, mit denen die zum Rendern einer Ansicht erforderliche Zeit reduziert wird.</span><span class="sxs-lookup"><span data-stu-id="028cc-359">The following table describes customizations that reduce the time that is required for a view to render.</span></span>
  
    
    

<span data-ttu-id="028cc-360">**Tabelle 8. Anpassungen, die den Zeitaufwand zum Rendern der Ansicht zu reduzieren.**</span><span class="sxs-lookup"><span data-stu-id="028cc-360">**Table 8. Customizations that reduce the time required for the view to render**</span></span>


|<span data-ttu-id="028cc-361">**Element**</span><span class="sxs-lookup"><span data-stu-id="028cc-361">**Item**</span></span>|<span data-ttu-id="028cc-362">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="028cc-362">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="028cc-363">Ansichtstyp</span><span class="sxs-lookup"><span data-stu-id="028cc-363">View type</span></span>  <br/> |<span data-ttu-id="028cc-364">Erstellen Sie eine Ansicht als Datenblattansicht und nicht als Standardansicht.</span><span class="sxs-lookup"><span data-stu-id="028cc-364">Create a view as a datasheet view instead of a standard view.</span></span>  <br/> |
|<span data-ttu-id="028cc-365">Ansicht: Elementgrenzwert</span><span class="sxs-lookup"><span data-stu-id="028cc-365">View: Item limit</span></span>  <br/> |<span data-ttu-id="028cc-p151">Alles über 1.000 wird wahrscheinlich langsam gerendert. Über eine langsame Verbindung ist es wichtig, zu der ein Gleichgewicht zwischen der Menge der Daten aufgeführt und die Anzahl von Roundtrips erforderlich sind, um alle Daten anzuzeigen. Je mehr Zeilen, die an eine Zeit, die weniger Roundtrips aber größere Seiten angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="028cc-p151">Anything over 1,000 will likely render slowly. Over a slow connection, it is important to experiment to find the right balance between the quantity of data shown at a time and the number of round trips necessary to view all the data. The more rows that display at a time, the fewer round trips, but larger pages.</span></span>  <br/> |
|<span data-ttu-id="028cc-369">Ansicht: Filter</span><span class="sxs-lookup"><span data-stu-id="028cc-369">View: Filter</span></span>  <br/> |<span data-ttu-id="028cc-p152">Verwenden Sie **[Today]** und **[Me]** -Schlüsselwörter, um Elemente nach Aktualität oder eine Zuordnung zu filtern. Verwenden Sie Statusfelder, um nur aktive Elemente in standardmäßigen Ansichten anzeigen. </span><span class="sxs-lookup"><span data-stu-id="028cc-p152">Use **[Today]** and **[Me]** keywords to filter items by freshness or assignment. Use Status fields to show only active items in default views. </span></span><br/> |
|<span data-ttu-id="028cc-372">Ansicht: Spalten</span><span class="sxs-lookup"><span data-stu-id="028cc-372">View: Columns</span></span>  <br/> |<span data-ttu-id="028cc-p153">Fügen Sie die kleinste Anzahl an Spalten ein. Erstellen Sie eine Standardansicht mit wenigen Spalten, die ein Browsen auf höchster Stufe ermöglicht, nachdem Benutzer ein Drilldown ausführen können.</span><span class="sxs-lookup"><span data-stu-id="028cc-p153">Include the smallest number of columns. Create a default view with few columns that allows high-level browsing after which people can drill down.</span></span>  <br/> |
   
<span data-ttu-id="028cc-p154">In der folgenden Tabelle sind die Anpassungen beschrieben, mit denen die zum Rendern einer Ansicht erforderliche Zeit erhöht wird. Mit jeder zusätzlichen Spalte wird die Renderingzeit um eine geringe Menge erhöht: bis zu einer halben Sekunde pro Spalte bei einer schnellen Netzwerkverbindung für eine Liste mit 1.000 Elementen. Wie in der Tabelle angemerkt ist, wird die Renderingzeit bei einigen Spalten mehr erhöht als bei anderen.</span><span class="sxs-lookup"><span data-stu-id="028cc-p154">The following table describes customizations that will increase the time that is required for a view to render. Each additional column increases rendering time by a slight amount: up to a half-second per column over a fast network connection for a list of 1,000 items. Some columns increase rendering time more than others, as noted in the table.</span></span>
  
    
    

<span data-ttu-id="028cc-378">**Tabelle 9. Anpassungen, die den Zeitaufwand zum Rendern der Ansicht erhöhen**</span><span class="sxs-lookup"><span data-stu-id="028cc-378">**Table 9. Customizations that increase the time required for the view to render**</span></span>


|<span data-ttu-id="028cc-379">**Element**</span><span class="sxs-lookup"><span data-stu-id="028cc-379">**Item**</span></span>|<span data-ttu-id="028cc-380">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="028cc-380">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="028cc-381">Gruppieren nach</span><span class="sxs-lookup"><span data-stu-id="028cc-381">Group By</span></span>  <br/> |<span data-ttu-id="028cc-p155">Beim Gruppieren werden HTML und JScript hinzugefügt, wodurch das Rendering für große Listen verlangsamt wird. Durch das standardmäßige Erweitern aller Gruppen wird die Renderingzeit aufgrund zusätzlicher Vorgänge im Browserobjektmodell weiter erhöht.</span><span class="sxs-lookup"><span data-stu-id="028cc-p155">Grouping adds HTML and JScript, which slows down rendering for large lists. Making all groups collapsed by default actually increases rendering time further because of additional operations on the browser object model.</span></span>  <br/> |
|<span data-ttu-id="028cc-384">Spalte - Titel über das Menü Bearbeiten mit einem Element verknüpft</span><span class="sxs-lookup"><span data-stu-id="028cc-384">Column - title linked to item with edit menu</span></span>  <br/> |<span data-ttu-id="028cc-385">Die Option "Titel über das Menü Bearbeiten mit einem Element verknüpft" dauert am längsten. Die ähnliche Option "Mit Element verknüpft" erhöht die Rendering-Zeit kaum.</span><span class="sxs-lookup"><span data-stu-id="028cc-385">The option "linked to item with edit menu" takes the longest; the similar option "linked to item" does not increase rendering time noticeably.</span></span>  <br/> |
   

## <a name="developer-dashboard"></a><span data-ttu-id="028cc-386">Entwicklerdashboard</span><span class="sxs-lookup"><span data-stu-id="028cc-386">Developer Dashboard</span></span>
<span data-ttu-id="028cc-387"><a name="DeveloperDashboard"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-387"></span></span>

<span data-ttu-id="028cc-p156">Das Entwicklerdashboard ist für SharePoint zum Bereitstellen weiterer Informationen, einschließlich MDS ein neu erstellt. Er ausgeführt wird, in einem separaten Fenster festzulegen, damit Rendering der aktuellen Seite und liefert ausführliche Anforderungsinformationen pro Seite mit einer Diagrammansicht. Darüber hinaus eine dedizierte Registerkarte für Protokolleinträge für eine bestimmte Anforderung Unified Logging System (ULS). Weitere detaillierte Informationen ist für die Analyse der Anforderung enthalten. Ablaufverfolgungsinformationen bieten einen dedizierten Windows Communication Foundation (WCF) Dienst (diagnosticsdata.svc) verwendet.</span><span class="sxs-lookup"><span data-stu-id="028cc-p156">The Developer Dashboard is rebuilt for SharePoint to provide more information, including MDS. It runs in a separate window to avoid affecting rendering of the actual page, and it provides detailed request information per page with a chart view. It also includes a dedicated tab for Unified Logging System (ULS) log entries for a particular request. Additional detailed information is included for request analysis. It uses a dedicated Windows Communication Foundation (WCF) service (diagnosticsdata.svc) designed to provide tracing information.</span></span>
  
    
    
<span data-ttu-id="028cc-393">Erfahren Sie mehr über das Entwicklerdashboard:</span><span class="sxs-lookup"><span data-stu-id="028cc-393">To learn more about the Developer Dashboard:</span></span>
  
    
    

-  <span data-ttu-id="028cc-394">[Übersicht über die SharePoint erneuert Entwicklerdashboard](http://www.microsoft.com/resources/technet/en-us/office/media/video/videol?cid=stc&amp;amp;from=mscomstc&amp;amp;VideoID=505bdd61-1fcc-4125-97fc-b5f0dda72cbc) (Video).</span><span class="sxs-lookup"><span data-stu-id="028cc-394">[Overview of the SharePoint renewed developer dashboard](http://www.microsoft.com/resources/technet/en-us/office/media/video/videol?cid=stc&amp;amp;from=mscomstc&amp;amp;VideoID=505bdd61-1fcc-4125-97fc-b5f0dda72cbc) (video).</span></span>
    
  
-  <span data-ttu-id="028cc-395">[Entwicklerdashboard erneuert](http://download.microsoft.com/download/7/7/3/773CA2C2-579B-408C-808E-A6F561194E20/Ig15_SP_IT_M10V3_devdash.pptx) (PowerPoint-Bildschirmpräsentation).</span><span class="sxs-lookup"><span data-stu-id="028cc-395">[Renewed Developer Dashboard](http://download.microsoft.com/download/7/7/3/773CA2C2-579B-408C-808E-A6F561194E20/Ig15_SP_IT_M10V3_devdash.pptx) (PowerPoint slide deck).</span></span>
    
  
<span data-ttu-id="028cc-396">Verwenden Sie zum Aktivieren des Entwicklerdashboards der folgende Codeausschnitt Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="028cc-396">To enable the Developer Dashboard, use the following Windows PowerShell snippet code.</span></span>
  
    
    



```

$content = ([Microsoft.SharePoint.Administration.SPWebService]::ContentService)
$appsetting =$content.DeveloperDashboardSettings
$appsetting.DisplayLevel = [Microsoft.SharePoint.Administration.SPDeveloperDashboardLevel]::On
$appsetting.Update() 

```

<span data-ttu-id="028cc-397">Abbildung 5 zeigt das Entwicklerdashboard.</span><span class="sxs-lookup"><span data-stu-id="028cc-397">Figure 5 shows the Developer Dashboard.</span></span>
  
    
    

<span data-ttu-id="028cc-398">**Abbildung 5. Entwicklerdashboard**</span><span class="sxs-lookup"><span data-stu-id="028cc-398">**Figure 5. Developer Dashboard**</span></span>

  
    
    

  
    
    
![Entwickler-Dashboard](../images/OptimizePage_Fig05_DevDashboard.png)
  
    
    
<span data-ttu-id="028cc-400">Es ist wichtig zu verstehen, wie diese Anfragen und die Anzahl der Bilder und Abfragen sich auf die Leistung auswirken.</span><span class="sxs-lookup"><span data-stu-id="028cc-400">It is important to understand how these requests and the number of images and queries affect performance.</span></span> <span data-ttu-id="028cc-401">Es gibt Ähnlichkeit zu serverseitig gerenderten Listenansichten (XSL oder CAML), da diese den gleichen Größenempfehlungen wie clientseitig gerenderte Listenansichten folgen.</span><span class="sxs-lookup"><span data-stu-id="028cc-401">There are similarities when it comes to server-side rendered list views (XSL or CAML) as they follow the same size recommendations as client-side rendered list views.</span></span> <span data-ttu-id="028cc-402">Die Serverlistenansicht-Anleitung ist jedoch nur für die Erstellung von Listenansichten für die Erfüllung Ihrer Anforderungen gedacht, wenn Ihr Ziel eine optimale Leistung ist, da Tausende von Ansichten aufgrund der Zwischenspeicherverwaltung eine höhere Leistungsminderung bedeuten.</span><span class="sxs-lookup"><span data-stu-id="028cc-402">However, server list view guidance is to create only list views necessary to accomplish your requirements when your goal is optimal performance, as thousands of views will cause greater degradation in performance due to compilation cache management.</span></span> <span data-ttu-id="028cc-403">Die physischen Merkmale des Computers, wie z. B. die Arbeitsspeicher- und Prozessorgeschwindigkeit, wirken sich auf die Gesamtgeschwindigkeit aus.</span><span class="sxs-lookup"><span data-stu-id="028cc-403">The physical characteristics of the computer, such as memory and processor speed, will factor into the overall speed.</span></span> <span data-ttu-id="028cc-404">Es muss berücksichtigt werden, wohin die Anforderungen weitergeleitet oder wie sie verteilt werden.</span><span class="sxs-lookup"><span data-stu-id="028cc-404">There is also consideration for where the requests route or how they are distributed.</span></span> <span data-ttu-id="028cc-405">Damit Sie besser verstehen, wie SharePoint Anforderungen weiterleitet und verteilt, können Sie das Anforderungs-Manager-Tool verwenden.</span><span class="sxs-lookup"><span data-stu-id="028cc-405">To better understand how SharePoint routes and distributes requests, you can use the Request Manager tool.</span></span> <span data-ttu-id="028cc-406">Eine detaillierte Erklärung der Anforderungsverteilung würde den Rahmen dieses Artikels sprengen.</span><span class="sxs-lookup"><span data-stu-id="028cc-406">However, discussing request distribution is beyond the scope of this article.</span></span> <span data-ttu-id="028cc-407">Weitere Informationen finden Sie unter [Konfigurieren des Anforderungs-Managers in SharePoint](http://technet.microsoft.com/library/jj712708.aspx).</span><span class="sxs-lookup"><span data-stu-id="028cc-407">For more information, see  [Configure Request Manager in SharePoint](http://technet.microsoft.com/library/jj712708.aspx).</span></span>
  
    
    

## <a name="conclusion"></a><span data-ttu-id="028cc-408">Schlussbemerkung</span><span class="sxs-lookup"><span data-stu-id="028cc-408">Conclusion</span></span>
<span data-ttu-id="028cc-409"><a name="bk_conclusion"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-409"></span></span>

<span data-ttu-id="028cc-p158">Ein Großteil der Richtlinien für die SharePoint 2010 Seite zur Optimierung der Leistung auf SharePoint angewendet wird. Dieser Artikel enthält einige der Elemente von Richtlinien für die SharePoint 2010 beim Einstieg in die neuen Bereiche, die speziell Leistung profitieren würden. Wir haben behandelt einige Verbesserungen, beispielsweise MDS und die erweiterte Entwicklerdashboard oder offensichtlich geändert wird. Wir mit der klassischen Anleitung eingeschlossen: Crunch nach unten JavaScript und cascading Stylesheets, ein CDN für allgemeine JavaScript Bibliotheken nach Möglichkeit zum Zwischenspeichern, kombinieren und Bilder so weit wie möglich komprimieren, beschränken oder Entfernen nicht benötigte Daten aus der Ansicht und erstellen Listenansichten überlegt, verwenden. Die Techniken und Funktionen, die in diesem Artikel erläuterten mitwirken für die Unterstützung der Leistungsziele.</span><span class="sxs-lookup"><span data-stu-id="028cc-p158">Much of the guidance for SharePoint 2010 page performance optimization applies to SharePoint. This article provides some of the elements of guidance for SharePoint 2010 while diving into new areas that would specifically benefit performance. We covered some obvious changes or enhancements, for example, MDS and the enhanced Developer Dashboard. We wrapped up with the classic guidance: crunch down JavaScript and cascading style sheets, use a CDN for common JavaScript libraries if possible for caching, combine and compress images as much as possible, limit or remove unnecessary data from view, and construct list views judiciously. The techniques and features discussed in this article contribute to supporting your performance goals.</span></span>
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="028cc-415">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="028cc-415">Additional resources</span></span>
<span data-ttu-id="028cc-416"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="028cc-416"></span></span>


-  [<span data-ttu-id="028cc-417">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="028cc-417">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="028cc-418">SharePoint Design Manager - Bilddarstellungen</span><span class="sxs-lookup"><span data-stu-id="028cc-418">SharePoint Design Manager image renditions</span></span>](sharepoint-design-manager-image-renditions.md)
    
  
-  [<span data-ttu-id="028cc-419">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="028cc-419">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="028cc-420">Übersicht über das SharePoint-Seitenmodell</span><span class="sxs-lookup"><span data-stu-id="028cc-420">Overview of the SharePoint page model</span></span>](overview-of-the-sharepoint-page-model.md)
    
  