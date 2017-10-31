---
title: "Designrichtlinien für die Benutzerfreundlichkeit von Add-Ins für SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.openlocfilehash: eaca30dd2bc29024ede688183cc6fd1fa5c34e7d
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="sharepoint-add-ins-ux-design-guidelines"></a><span data-ttu-id="177fe-102">Designrichtlinien für die Benutzerfreundlichkeit von Add-Ins für SharePoint</span><span class="sxs-lookup"><span data-stu-id="177fe-102">SharePoint Add-ins UX design guidelines</span></span>
<span data-ttu-id="177fe-103">Hier erhalten Sie Informationen über allgemeine, auf das Benutzungserlebnis bzw. die User Experience (UX) ausgerichtete Entwurfsrichtlinien für Add-Ins in SharePoint, darunter die Wahl des Chrom, die Verwendung des CSS, das Verwalten von Benutzerlizenzen und andere Entwurfsaufgaben.</span><span class="sxs-lookup"><span data-stu-id="177fe-103">Learn about general user experience (UX) design guidelines for add-ins in SharePoint, including choosing the chrome, using CSS, managing user licenses, and other design tasks.</span></span>
 

 <span data-ttu-id="177fe-p101">**Hinweis** Der Name „Apps für SharePoint“ wird in „SharePoint-Add-Ins“ geändert. Während des Übergangszeitraums wird in der Dokumentation und der Benutzeroberfläche einiger SharePoint-Produkte und Visual Studio-Tools möglicherweise weiterhin der Begriff „Apps für SharePoint“ verwendet. Weitere Informationen finden Sie unter [Neuer Name für Office- und SharePoint-Apps](new-name-for-apps-for-sharepoint.md#bk_newname).</span><span class="sxs-lookup"><span data-stu-id="177fe-p101">**Note**  The name "apps for SharePoint" is changing to "SharePoint Add-ins". During the transition, the documentation and the UI of some SharePoint products and Visual Studio tools might still use the term "apps for SharePoint". For details, see  [New name for apps for Office and SharePoint](new-name-for-apps-for-sharepoint.md#bk_newname).</span></span>
 

<span data-ttu-id="177fe-p102">Add-Ins sind ein neues Konzept für SharePoint und ermöglichen Endbenutzern, ihren Websites neue Funktionen hinzuzufügen und dabei die Zuverlässigkeit der SharePoint-Site weiterhin zu gewährleisten. Zum Erstellen eines guten Add-Ins gehört nicht nur, interessante Funktionen bereitzustellen (obwohl dies ebenfalls wichtig ist), sondern auch sicherzustellen, dass das Add-In gut aussieht und sich nahtlos in die Website, auf der es installiert wird, einfügt.</span><span class="sxs-lookup"><span data-stu-id="177fe-p102">Add-ins are a new concept for SharePoint, empowering end users to add new functionality to their sites while still ensuring reliability for the SharePoint site itself. Creating a good add-in requires not only making great functionality (although that's obviously important), but also ensuring that the add-in looks right and fits seamlessly into the site where it's installed.</span></span>
 

## <a name="choosing-the-chrome-for-your-add-in"></a><span data-ttu-id="177fe-109">Wahl des Chrom für Ihr Add-In</span><span class="sxs-lookup"><span data-stu-id="177fe-109">Choosing the chrome for your add-in</span></span>
<span data-ttu-id="177fe-110"><a name="UXGuide_AppChrome"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-110"><a name="UXGuide_AppChrome"> </a></span></span>

<span data-ttu-id="177fe-p103">Beim Erstellen eines Add-Ins müssen Sie als erstes entscheiden, wie ausgeprägt das Branding Ihrer Seiten sein soll und wo diese gehostet werden sollen. Auf der Grundlage dieser Optionen liegt es dann auf der Hand, welche Technologie Sie für den Betrieb Ihres Chrom verwenden:</span><span class="sxs-lookup"><span data-stu-id="177fe-p103">The first thing you have to determine when you are building an add-in is how much or how little you want to brand your pages and where you want them to be hosted. Depending on those choices, which technology you use to power your chrome will be relatively obvious:</span></span>
 

 

-  <span data-ttu-id="177fe-113">**In SharePoint gehostete ASPX-Seiten:** Verwenden Sie die Add-In-Vorlage.</span><span class="sxs-lookup"><span data-stu-id="177fe-113">**ASPX pages hosted in SharePoint:** Use the add-in template.</span></span>
    
 
-  <span data-ttu-id="177fe-114">**In SharePoint gehostete HTML-Seiten oder beliebige Seiten außerhalb von SharePoint:** Verwenden Sie das Chromsteuerelement.</span><span class="sxs-lookup"><span data-stu-id="177fe-114">**HTML pages hosted in SharePoint or any pages outside SharePoint:** Use the chrome control.</span></span>
    
 
-  <span data-ttu-id="177fe-115">**Seiten mit benutzerdefiniertem Branding:** Verwenden Sie ein eigenes Chrom.</span><span class="sxs-lookup"><span data-stu-id="177fe-115">**Custom branded pages:** Use your own chrome.</span></span>
    
 

### <a name="using-the-add-in-template-for-sharepoint-hosted-pages"></a><span data-ttu-id="177fe-116">Verwenden der Add-In-Vorlage für in SharePoint gehostete Seiten</span><span class="sxs-lookup"><span data-stu-id="177fe-116">Using the add-in template for SharePoint-hosted pages</span></span>
<span data-ttu-id="177fe-117"><a name="UXGuide_AppTemplate"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-117"><a name="UXGuide_AppTemplate"> </a></span></span>

<span data-ttu-id="177fe-p104">Die Add-In-Vorlage kann nur für in SharePoint gehostete ASPX-Seiten verwendet werden. Die Vorlage enthält die **app.master**-Masterseite (die für ein Add-In geeignetes Chrom enthält und auf das Design der Hostwebsite abgestimmt ist), und verbirgt SharePoint-Funktionen, die entweder nicht funktionieren würden oder innerhalb einer Add-In-Web nicht sinnvoll sind. Abbildung 1 zeigt eine in SharePoint gehostete Seite, die die Add-In-Vorlage verwendet.</span><span class="sxs-lookup"><span data-stu-id="177fe-p104">The add-in template can be used only for SharePoint-hosted ASPX pages. The template includes the  **app.master** master page (which contains chrome appropriate for an add-in and is designed to theme with the host site), and it hides some SharePoint functionality that either wouldn't work or doesn't make sense inside of an add-in web. Figure 1 shows a SharePoint-hosted page that uses the add-in template.</span></span>
 

 

<span data-ttu-id="177fe-121">**Abbildung 1. In SharePoint gehostete Seite, die die Add-In-Vorlage verwendet**</span><span class="sxs-lookup"><span data-stu-id="177fe-121">**Figure 1. SharePoint-hosted page using the add-in template**</span></span>

 

 
![Eine in SharePoint gehostete Seite, die die App-Vorlage verwendet](../images/AppUXGuidelines_AppTemplate.png)
 
<span data-ttu-id="177fe-123">Die Add-In-Vorlage ist die Standardvorlage in Visual Studio, wenn Sie eine Add-In-Website und Seiten innerhalb dieser Website erstellen.</span><span class="sxs-lookup"><span data-stu-id="177fe-123">The add-in template is the default in Visual Studio when you create an add-in web and pages within that web.</span></span>
 

 

### <a name="using-the-chrome-control-in-sharepoint-add-ins"></a><span data-ttu-id="177fe-124">Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-124">Using the chrome control in SharePoint Add-ins</span></span>
<span data-ttu-id="177fe-125"><a name="UXGuide_ChromeControl"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-125"><a name="UXGuide_ChromeControl"> </a></span></span>

<span data-ttu-id="177fe-p105">Wenn Sie keine in SharePoint gehosteten ASPX-Seiten erstellen, Ihr Add-In sich jedoch trotzdem problemlos in die Hostwebsite, von der aus es verwendet wird, einbinden lassen soll, ist das Chromsteuerelement die richtige Wahl. Abbildung 2 zeigt das Chromsteuerelement.</span><span class="sxs-lookup"><span data-stu-id="177fe-p105">If you're not building SharePoint-hosted ASPX pages, but you still want your add-in to fit in naturally with the host site that it is used from, the chrome control is the right choice. Figure 2 shows the chrome control.</span></span>
 

 

<span data-ttu-id="177fe-128">**Abbildung 2. Chromsteuerelement auf einer Webseite**</span><span class="sxs-lookup"><span data-stu-id="177fe-128">**Figure 2. Chrome control in a webpage**</span></span>

 

 
![Chromsteuerelement auf einer Webseite](../images/AppUXGuidelines_ChromeControl.png)
 

 

 

<span data-ttu-id="177fe-130">**Video ansehen: SharePoint-Chromsteuerelement**</span><span class="sxs-lookup"><span data-stu-id="177fe-130">**Watch the video: SharePoint chrome control**</span></span>

 

 
![Videos](../images/mod_icon_video.png)
 

 

 

 

 

### <a name="to-use-the-chrome-control"></a><span data-ttu-id="177fe-132">So verwenden Sie das Chromsteuerelement</span><span class="sxs-lookup"><span data-stu-id="177fe-132">To use the chrome control</span></span>


1. <span data-ttu-id="177fe-p106">Fügen Sie der Steuerelementbibliothek einen Verweis hinzu. Hierzu stehen Ihnen zwei Möglichkeiten zur Verfügung:</span><span class="sxs-lookup"><span data-stu-id="177fe-p106">Add a reference to the controls library. There are two ways to do this:</span></span>
    
      - <span data-ttu-id="177fe-135">Verweisen Sie im Stamm des Layouts-Ordners auf die Bibliothek, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="177fe-135">Point to the library at the root of the layouts folder, as shown in the following example.</span></span>
    
```
  <script 
    type="text/javascript" 
    src="http://{server URL}/_layouts/15/sp.ui.controls.js">
</script>
```

  - <span data-ttu-id="177fe-136">Kopieren Sie die Bibliothek auf Ihre eigene Website und verweisen Sie dort auf sie.</span><span class="sxs-lookup"><span data-stu-id="177fe-136">Copy the library to your own website, and reference it from there.</span></span>
    
     <span data-ttu-id="177fe-137">**Vorsicht** Wenn Sie sich für diese Alternative entscheiden, kann Ihr Add-In keine Aktualisierungen des Steuerelements nutzen</span><span class="sxs-lookup"><span data-stu-id="177fe-137">**Caution**  If you opt for this alternative your add-in will not benefit from updates to the control.</span></span>
2. <span data-ttu-id="177fe-138">Fügen Sie das DOM-Platzhalterelement an der Position ein, an der das Steuerelement gerendert werden soll, wie in diesem Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="177fe-138">Add the placeholder DOM element where the control will be rendered, as shown in this example.</span></span>
    
```
  <div id='chromeControlContainer'></div>
```

3. <span data-ttu-id="177fe-139">Instanziieren Sie das Steuerelement.</span><span class="sxs-lookup"><span data-stu-id="177fe-139">Instantiate the control.</span></span>
    
```
  function addchromecontrol(){
    var options = {};
    options.siteTitle ="{host site title}";
    options.siteUrl = "{host URL}";
    options.appHelpPageUrl = "{help page URL}";
    options.appIconUrl = "{app icon URL}";
    options.appTitle = "add-in Title";
    nav = new SP.UI.Controls.Navigation("chromeControlContainer", options);
    nav.setVisible(true);
}
```

4. <span data-ttu-id="177fe-140">(Optional) Wenn Sie keinen Titelbereich auf Ihrer Seite möchten, können Sie ihn entfernen, indem Sie den folgenden JavaScript-Code ausführen.</span><span class="sxs-lookup"><span data-stu-id="177fe-140">(Optional) If you don't want to have the title area on your page, you can remove it by running the following JavaScript code.</span></span>
    
```
  nav.setBottomHeaderVisible(false);
```

<span data-ttu-id="177fe-p107">Das Chromsteuerelement bietet zwei optionale Add-In-Symbole: Eines in der oberen Navigationsleiste und eines im Titelbereich. Das Add-In-Symbol in der oberen Navigationsleiste umfasst 24 x 24 Pixel (px), das Symbol im Titelbereich hat die gleiche Größe wie SharePoint-Website-Symbole - max. 64 px auf 180 px. Es wird empfohlen, ein auf einem weißen, schwarzen, grauen, hellen und gedeckten Hintergrund getestetes PNG-Bild zu verwenden, da Benutzer und Administratoren das Websitedesign ändern können. Weitere Informationen über die Verwendung des Chromsteuerelements finden Sie unter  [Verwenden des Client-Chromsteuerelements in Add-Ins für SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="177fe-p107">The chrome control provides for two optional add-in icons: one on the top navigation bar and one in the title area. The add-in icon on the top navigation bar is 24 x 24 pixels (px), and the icon in the title area is the same size as SharePoint site icons—up to 64 px high by up to 180 px long. We recommend you use a PNG image that you have tested on white, black, gray, bright, and muted backgrounds because users and admins can change the site theme. For more information about using the chrome control, see  [Use the client chrome control in SharePoint Add-ins](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span></span>
 

 

### <a name="creating-a-custom-branded-ui-in-sharepoint-add-ins"></a><span data-ttu-id="177fe-145">Erstellen ein benutzerdefiniertes Branding-Benutzeroberfläche in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-145">Creating a custom branded UI in SharePoint Add-ins</span></span>
<span data-ttu-id="177fe-146"><a name="UXGuide_CustomUI"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-146"><a name="UXGuide_CustomUI"> </a></span></span>

<span data-ttu-id="177fe-p108">Wenn Sie Ihr eigenes Branding im Add-In verwenden möchten, anstatt sie am Design der Hostwebsite auszurichten und in die SharePoint-Site einzupassen, in der Ihr Add-In installiert ist, müssen Sie das Chromsteuerelement vollständig neu erstellen. Sie sollten jedoch noch einen Link „Zurück zur Website" in der linken oberen Ecke der Seite (oben rechts bei Sprachen, die von rechts nach links gelesen werden) vorsehen, über den der Benutzer zurück zu der Website gelangen kann, auf der das Add-In installiert ist.</span><span class="sxs-lookup"><span data-stu-id="177fe-p108">If, instead of aligning to the host site's theme and fitting into the SharePoint site where your add-in is installed, you want to use your own brand inside your add-in, you will have to build your chrome from scratch. However, you should still have a "back to site" link in the upper-left corner of the page (upper-right in right-to-left [RTL] languages) that redirects the user back to the site where the add-in is installed.</span></span>
 

 

## <a name="using-the-host-web-css-in-sharepoint-add-ins"></a><span data-ttu-id="177fe-149">Verwenden des Hostweb-CSS in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-149">Using the host web CSS in SharePoint Add-ins</span></span>
<span data-ttu-id="177fe-150"><a name="UXGuide_CSS"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-150"><a name="UXGuide_CSS"> </a></span></span>

<span data-ttu-id="177fe-p109">Indem Sie die gleichen Formate wie für die Hostwebsite verwenden, können Sie sicherstellen, dass Ihre Add-Ins mit der SharePoint-Website konsistent bleiben, aus der sie stammen. Die tatsächlichen Formate können sich basierend auf dem Design der Website ändern. Indem Sie jedoch auf die CSS-Datei der Hostwebsite verweisen, können Sie sicher sein, dass Ihr Add-In sich unabhängig von seinem Installationsort einfügt.</span><span class="sxs-lookup"><span data-stu-id="177fe-p109">By using the same styles that are used on the host web, you can ensure that your add-ins will remain consistent with the SharePoint site that they came from. The actual styles may change based on the design of the site, but by referencing the CSS file of the host web, you will know that your add-in will fit in no matter where it's installed.</span></span>
 

 
<span data-ttu-id="177fe-p110">Um die CSS-Formatvorlagen von der Hostwebsite abzurufen, müssen Sie auf ihre CSS-Datei verweisen. Dazu gibt es verschiedene Möglichkeiten.</span><span class="sxs-lookup"><span data-stu-id="177fe-p110">To get the CSS styles from the host web, you have to reference its CSS file. You can do this in several different ways.</span></span>
 

 

### <a name="to-reference-the-host-webs-css-file"></a><span data-ttu-id="177fe-155">So verweisen Sie auf die CSS-Datei der Hostwebsite</span><span class="sxs-lookup"><span data-stu-id="177fe-155">To reference the host web's CSS file</span></span>


1. <span data-ttu-id="177fe-156">Wenn Sie die Add-In-Vorlage oder das Add-In-Chromsteuerelement verwenden, wird dies automatisch für Sie erledigt.</span><span class="sxs-lookup"><span data-stu-id="177fe-156">If you're using the add-in template or add-in chrome control, this is automatically taken care of for you.</span></span>
    
 
2. <span data-ttu-id="177fe-157">Wenn Sie sich innerhalb der Add-In-Website befinden, können Sie die Steuerelemente **CssRegistration** und **CssLink** verwenden, um auf die CSS-Datei zu verweisen, indem Sie den folgenden Code entweder auf der Masterseite oder der ASPX-Seite einfügen:</span><span class="sxs-lookup"><span data-stu-id="177fe-157">If you're inside the add-in web, you can use the  **CssRegistration** and **CssLink** controls to reference the CSS file by putting the following code on either your master page or ASPX page:</span></span>
    
```HTML
  <SharePoint:CssRegistration runat="server" name="default" />
<SharePoint:CssLink runat="server />

```

3. <span data-ttu-id="177fe-158">Sie können ein <link>-Element verwenden, um auf die CSS-Datei zu verweisen, indem Sie eine URL aus der URL der Hostwebsite erstellen, wie in diesem Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="177fe-158">You can use a <link> element to reference the CSS file by building a URL off of the host web's URL, as shown in this example.</span></span>
    
```HTML
  <link rel="stylesheet" href="{host web URL}/_layouts/15/defaultcss.ashx" />
```


    If you use this approach, you have to run JavaScript in the page to get the host web's URL off the query string. Then you can insert the host web's URL into the  **link** element before you write the element to the page's DOM.
    
 
<span data-ttu-id="177fe-p111">Als erstes sollten Sie beim Formatieren Ihres Add-Ins möglichst viel semantischen HTML-Code verwenden, d. h. **H1**, **H2**, **H3** usw. für die verschiedenen Überschriften und Eingabetags für Schaltflächen. Sie sollten außerdem versuchen, in möglichst großem Umfang SharePoint-Kernformatvorlagen zu verwenden, damit bei einer Änderung des Designs der Hostwebsite Ihr Add-In diese Änderungen nahtlos und automatisch übernimmt. Die folgenden Tabellen zeigen die Verwendung von Formatvorlagen beim Standarddesign.</span><span class="sxs-lookup"><span data-stu-id="177fe-p111">The first thing to do when you are styling your add-in is to use semantic HTML as much as possible. That means using  **H1**,  **H2**,  **H3**, and so on, for the various headings, and input tags for buttons. You should also try to use SharePoint core styles as much as possible so that when the theme of the host site changes, your add-in picks up those changes seamlessly and automatically. The following tables show how styles are used in the default theme.</span></span>
 

 

<span data-ttu-id="177fe-163">**Tabelle 1. Textkörperformatvorlagen**</span><span class="sxs-lookup"><span data-stu-id="177fe-163">**Table 1. Body text styles**</span></span>


|<span data-ttu-id="177fe-164">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="177fe-164">**Example**</span></span>|<span data-ttu-id="177fe-165">**Verwendet für**</span><span class="sxs-lookup"><span data-stu-id="177fe-165">**Used for**</span></span>|<span data-ttu-id="177fe-166">**Format**</span><span class="sxs-lookup"><span data-stu-id="177fe-166">**Style**</span></span>|
|:-----|:-----|:-----|
|![ms-textXLarge](../images/AppUXGuidelines_ms-textxlarge.png)|<span data-ttu-id="177fe-168">Besonders großer Textkörper</span><span class="sxs-lookup"><span data-stu-id="177fe-168">Extra large body text</span></span>|<span data-ttu-id="177fe-169">.ms-textXLarge</span><span class="sxs-lookup"><span data-stu-id="177fe-169">.ms-textXLarge</span></span>|
|![ms-textlarge](../images/AppUXGuidelines_ms-textlarge.png)|<span data-ttu-id="177fe-171">Großer Textkörper</span><span class="sxs-lookup"><span data-stu-id="177fe-171">Large body text</span></span>|<span data-ttu-id="177fe-172">.ms-textLarge</span><span class="sxs-lookup"><span data-stu-id="177fe-172">.ms-textLarge</span></span>|
|![body](../images/AppUXGuidelines_body.png)|<span data-ttu-id="177fe-174">Normaler Textkörper</span><span class="sxs-lookup"><span data-stu-id="177fe-174">Normal body text</span></span>|<span data-ttu-id="177fe-175">Wird automatisch geerbt</span><span class="sxs-lookup"><span data-stu-id="177fe-175">Inherited automatically</span></span>|
|![ms-textsmall](../images/AppUXGuidelines_ms-textsmall.png)|<span data-ttu-id="177fe-177">Kleiner Textkörper</span><span class="sxs-lookup"><span data-stu-id="177fe-177">Small body text</span></span>|<span data-ttu-id="177fe-178">.ms-textSmall</span><span class="sxs-lookup"><span data-stu-id="177fe-178">.ms-textSmall</span></span>|
|![ms-metadata](../images/AppUXGuidelines_ms-metadata.png)|<span data-ttu-id="177fe-180">Metadatentext</span><span class="sxs-lookup"><span data-stu-id="177fe-180">Metadata text</span></span>|<span data-ttu-id="177fe-181">.ms-metadata</span><span class="sxs-lookup"><span data-stu-id="177fe-181">.ms-metadata</span></span>|

<span data-ttu-id="177fe-182">**Tabelle 2. Titel- und Überschriftenformatvorlagen**</span><span class="sxs-lookup"><span data-stu-id="177fe-182">**Table 2. Title and header styles**</span></span>


|<span data-ttu-id="177fe-183">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="177fe-183">**Example**</span></span>|<span data-ttu-id="177fe-184">**Verwendet für**</span><span class="sxs-lookup"><span data-stu-id="177fe-184">**Used for**</span></span>|<span data-ttu-id="177fe-185">**Format**</span><span class="sxs-lookup"><span data-stu-id="177fe-185">**Style**</span></span>|
|:-----|:-----|:-----|
|![ms-core-pagetitle](../images/AppUXGuidelines_ms-core-pagetitle.png)|<span data-ttu-id="177fe-187">Haupttitel auf der Seite</span><span class="sxs-lookup"><span data-stu-id="177fe-187">Main title on the page</span></span>|<span data-ttu-id="177fe-188">.ms-core-pageTitle</span><span class="sxs-lookup"><span data-stu-id="177fe-188">.ms-core-pageTitle</span></span>|
|![h1](../images/AppUXGuidelines_h1.png)|<span data-ttu-id="177fe-p112">Titel für Dialogfelder, Formulare, Blogs und Diskussionsbeiträge. Ein alternativer „primärer“ Titel für spezielle Inhaltstypen oder Add-Ins, die die ganze Seite einnehmen und sich von einer regulären Wiki- oder Webparts-Seite unterscheiden sollen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p112">Title for dialog boxes, forms, blogs, and discussion posts. It's an alternative "primary" title for special content types or add-ins that take up the entire pagethat you want to be different from a regular wiki or Web Parts page.</span></span>|<span data-ttu-id="177fe-192">H1</span><span class="sxs-lookup"><span data-stu-id="177fe-192">H1</span></span>|
|![h2](../images/AppUXGuidelines_h2.png)|<span data-ttu-id="177fe-p113">Sekundäre Überschrift im Verhältnis zu H1. Zum Beispiel verwendet Communitys H1 Accent für den Titel eines Beitrags und H2 Accent für die beste "Antwort" auf den Beitrag.</span><span class="sxs-lookup"><span data-stu-id="177fe-p113">Secondary heading in relation to H1. For example, Communities uses H1 Accent for the title of a post, and H2 Accent for the best "response" to the post.</span></span>|<span data-ttu-id="177fe-196">H2</span><span class="sxs-lookup"><span data-stu-id="177fe-196">H2</span></span>|
|![h3](../images/AppUXGuidelines_h3.png)|<span data-ttu-id="177fe-198">In der Regel eine Unterüberschrift unter H2.</span><span class="sxs-lookup"><span data-stu-id="177fe-198">Generally a subheading under H2.</span></span>|<span data-ttu-id="177fe-199">H3</span><span class="sxs-lookup"><span data-stu-id="177fe-199">H3</span></span>|
|![h4](../images/AppUXGuidelines_h4.png)|<span data-ttu-id="177fe-201">Unterüberschriften unter H3.</span><span class="sxs-lookup"><span data-stu-id="177fe-201">Subheadings under H3.</span></span>|<span data-ttu-id="177fe-202">H4</span><span class="sxs-lookup"><span data-stu-id="177fe-202">H4</span></span>|
|![ms-webpart-titletext](../images/AppUXGuidelines_ms-webpart-titletext.png)|<span data-ttu-id="177fe-204">Titel des Haupt- bzw. primären Webparts auf einer Seite oder für Hauptabschnittsüberschriften.</span><span class="sxs-lookup"><span data-stu-id="177fe-204">Title of the main/primary Web Part on a page, or for main section headers.</span></span>|<span data-ttu-id="177fe-205">.ms-webpart-titleText</span><span class="sxs-lookup"><span data-stu-id="177fe-205">.ms-webpart-titleText</span></span>|
|![ms-dlg-heading](../images/AppUXGuidelines_ms-dlg-heading.png)|<span data-ttu-id="177fe-207">Titel für Überschriften in Dialogfeldern oder Legenden.</span><span class="sxs-lookup"><span data-stu-id="177fe-207">Title for headings within dialog boxes or callouts.</span></span>|<span data-ttu-id="177fe-208">.ms-dlg-heading</span><span class="sxs-lookup"><span data-stu-id="177fe-208">.ms-dlg-heading</span></span>|

<span data-ttu-id="177fe-209">**Tabelle 3. Formatvorlagen für die Navigation**</span><span class="sxs-lookup"><span data-stu-id="177fe-209">**Table 3. Navigation styles**</span></span>


|<span data-ttu-id="177fe-210">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="177fe-210">**Example**</span></span>|<span data-ttu-id="177fe-211">**Verwendet für**</span><span class="sxs-lookup"><span data-stu-id="177fe-211">**Used for**</span></span>|<span data-ttu-id="177fe-212">**Format**</span><span class="sxs-lookup"><span data-stu-id="177fe-212">**Style**</span></span>|
|:-----|:-----|:-----|
|![QuickLaunchHeading](../images/AppUXGuidelines_QuickLaunchHeading.png)|<span data-ttu-id="177fe-214">Überschrift der linken Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="177fe-214">Heading of the left navigation bar.</span></span>|<span data-ttu-id="177fe-215">.ms-core-listMenu-verticalBox > .ms-core-listMenu-root > li > .ms-core-listMenu-item</span><span class="sxs-lookup"><span data-stu-id="177fe-215">.ms-core-listMenu-verticalBox > .ms-core-listMenu-root > li > .ms-core-listMenu-item</span></span>|
|![QuickLaunchLink](../images/AppUXGuidelines_QuickLaunchLink.png)|<span data-ttu-id="177fe-217">Link in der linken Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="177fe-217">Link in the left navigation bar.</span></span>|<span data-ttu-id="177fe-218">.ms-core-listMenu-verticalBox</span><span class="sxs-lookup"><span data-stu-id="177fe-218">.ms-core-listMenu-verticalBox</span></span>|
|![QuickLaunchSelected](../images/AppUXGuidelines_QuickLaunchSelected.png)|<span data-ttu-id="177fe-220">Ausgewähltes Element in der linken Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="177fe-220">Selected item in the left navigation bar.</span></span>|<span data-ttu-id="177fe-221">.ms-core-listMenu-verticalBox + .ms-accentText</span><span class="sxs-lookup"><span data-stu-id="177fe-221">.ms-core-listMenu-verticalBox + .ms-accentText</span></span>|
|![TopNav](../images/AppUXGuidelines_TopNav.png)|<span data-ttu-id="177fe-223">Element in der oberen Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="177fe-223">Item in the top navigation bar.</span></span>||
|![TopNavSelected](../images/AppUXGuidelines_TopNavSelected.png)|<span data-ttu-id="177fe-225">Ausgewähltes Element in der oberen Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="177fe-225">Selected item in the top navigation bar.</span></span>||

<span data-ttu-id="177fe-226">**Tabelle 4. Formatvorlagen für Befehle**</span><span class="sxs-lookup"><span data-stu-id="177fe-226">**Table 4. Command styles**</span></span>


|<span data-ttu-id="177fe-227">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="177fe-227">**Example**</span></span>|<span data-ttu-id="177fe-228">**Verwendet für**</span><span class="sxs-lookup"><span data-stu-id="177fe-228">**Used for**</span></span>|<span data-ttu-id="177fe-229">**Format**</span><span class="sxs-lookup"><span data-stu-id="177fe-229">**Style**</span></span>|
|:-----|:-----|:-----|
|![ms-commandlink](../images/AppUXGuidelines_ms-commandlink.png)|<span data-ttu-id="177fe-p114">Links für primäre Aktionen, die der Benutzer innerhalb eines bestimmten Containers oder einer Seite durchführen soll. Wird z. B. verwendet, um die Befehle unter einer Legende zu formatieren. Zeigt immer die gleiche Farbe für besuchte und nicht besuchte Befehle an.</span><span class="sxs-lookup"><span data-stu-id="177fe-p114">Primary action links you expect the user to take within a given container or page. For example, this would be used to style the commands underneath a callout. This will always be the same color for visited and non-visited commands.</span></span>|<span data-ttu-id="177fe-234">.ms-commandLink</span><span class="sxs-lookup"><span data-stu-id="177fe-234">.ms-commandLink</span></span>|
|![ms-secondarycommandlink](../images/AppUXGuidelines_ms-secondarycommandlink.png)|<span data-ttu-id="177fe-p115">Wird auch zum Formatieren von Aktions-Links verwendet, jedoch für Aktionen, die für den Inhalt sekundär sind. Diese Formatvorlage wird für sekundäre Aktionen verwendet, damit sie nicht die Aufmerksamkeit vom Inhalt ablenken.</span><span class="sxs-lookup"><span data-stu-id="177fe-p115">Also used to style action links, but for actions that are secondary to the content. This style is used for these secondary actions, so they don't compete with content for attention.</span></span>|<span data-ttu-id="177fe-238">.ms-secondaryCommandLink</span><span class="sxs-lookup"><span data-stu-id="177fe-238">.ms-secondaryCommandLink</span></span>|
|![ms-calloutlink](../images/AppUXGuidelines_ms-calloutlink.png)|<span data-ttu-id="177fe-240">Links in der Legende.</span><span class="sxs-lookup"><span data-stu-id="177fe-240">Links in the callout.</span></span>|<span data-ttu-id="177fe-241">.ms-calloutLink</span><span class="sxs-lookup"><span data-stu-id="177fe-241">.ms-calloutLink</span></span>|

<span data-ttu-id="177fe-242">**Tabelle 5. Formatvorlagen für Modifzierer**</span><span class="sxs-lookup"><span data-stu-id="177fe-242">**Table 5. Modifier styles**</span></span>


|<span data-ttu-id="177fe-243">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="177fe-243">**Example**</span></span>|<span data-ttu-id="177fe-244">**Verwendet für**</span><span class="sxs-lookup"><span data-stu-id="177fe-244">**Used for**</span></span>|<span data-ttu-id="177fe-245">**Format**</span><span class="sxs-lookup"><span data-stu-id="177fe-245">**Style**</span></span>|
|:-----|:-----|:-----|
|![ms-accenttext](../images/AppUXGuidelines_ms-accenttext.png)|<span data-ttu-id="177fe-247">Hilfsklasse, die die Akzentfarbe aus dem aktuellen Design für Text bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="177fe-247">Helper class that will provide the accent color from the current theme for text.</span></span>|<span data-ttu-id="177fe-248">.ms-accentText</span><span class="sxs-lookup"><span data-stu-id="177fe-248">.ms-accentText</span></span>|
|![Link](../images/AppUXGuidelines_hyperlink.png)|<span data-ttu-id="177fe-p116">Links im Inhalt sollten vom Hyperlinkformat und -verhalten erben. Das Hyperlinkformat wendet eine Farbe und einen Hover-Effekt an, um anzugeben, dass es sich um einen Link und nicht um normalen Text handelt.</span><span class="sxs-lookup"><span data-stu-id="177fe-p116">Links in the content should inherit from default hyperlink styling and behavior. Hyperlink styling applies a color and a hover effect to indicate that it's a link instead of normal text.</span></span>|<span data-ttu-id="177fe-252">Durch Verwenden von <a> geerbt.</span><span class="sxs-lookup"><span data-stu-id="177fe-252">Inherited from using <a>.</span></span>|
|![ms-error](../images/AppUXGuidelines_ms-error.png)|<span data-ttu-id="177fe-254">Fehlermeldungen in Formularen.</span><span class="sxs-lookup"><span data-stu-id="177fe-254">Error messages that occur in forms.</span></span>|<span data-ttu-id="177fe-255">.ms-error</span><span class="sxs-lookup"><span data-stu-id="177fe-255">.ms-error</span></span>|
|![ms-soften](../images/AppUXGuidelines_ms-soften.png)|<span data-ttu-id="177fe-257">Hilfsklasse, die ein schattiertes Grau für Text bereitstellt, der weniger hervorgehoben sein soll wie der normale Textkörper.</span><span class="sxs-lookup"><span data-stu-id="177fe-257">Helper class that provides a softened gray for text that should be less emphasized than normal body text.</span></span>|<span data-ttu-id="177fe-258">.ms-soften</span><span class="sxs-lookup"><span data-stu-id="177fe-258">.ms-soften</span></span>|
|![ms-disabled](../images/AppUXGuidelines_ms-disabled.png)|<span data-ttu-id="177fe-260">Hilfsklasse, welche die "deaktivierte" Farbe auf Text anwendet, der zur Kennzeichnung von deaktivierten Stati verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="177fe-260">Helper class that applies the "disabled" color to text, which is used for denoting disabled states.</span></span>|<span data-ttu-id="177fe-261">.ms-disabled</span><span class="sxs-lookup"><span data-stu-id="177fe-261">.ms-disabled</span></span>|
|![ms-uppercase](../images/AppUXGuidelines_ms-uppercase.png)|<span data-ttu-id="177fe-263">Hilfsklasse, die den Text vollständig in Großbuchstaben umwandelt.</span><span class="sxs-lookup"><span data-stu-id="177fe-263">Helper class that transforms the text to all caps.</span></span>|<span data-ttu-id="177fe-264">.ms-uppercase</span><span class="sxs-lookup"><span data-stu-id="177fe-264">.ms-uppercase</span></span>|
|![ms-helper](../images/AppUXGuidelines_ms-helper.png)|<span data-ttu-id="177fe-266">Hilfsklasse zum Formatieren von Text wie Formulare.</span><span class="sxs-lookup"><span data-stu-id="177fe-266">Helper class to style text like forms.</span></span>|<span data-ttu-id="177fe-267">.ms-helper</span><span class="sxs-lookup"><span data-stu-id="177fe-267">.ms-helper</span></span>|
|![hr](../images/AppUXGuidelines_hr.png)|<span data-ttu-id="177fe-269">Gestrichelte Trennlinie, die verwendet wird, um Abschnitte im Schnellstartbereich und in Menüs zu trennen.</span><span class="sxs-lookup"><span data-stu-id="177fe-269">Dashed line divider that is used to divide sections in the Quick Launch and in menus.</span></span>|<span data-ttu-id="177fe-270">HR</span><span class="sxs-lookup"><span data-stu-id="177fe-270">HR</span></span>|

<span data-ttu-id="177fe-271">**Tabelle 6. Formatvorlagen für Part-Benutzeroberflächen**</span><span class="sxs-lookup"><span data-stu-id="177fe-271">**Table 6. Part user interface styles**</span></span>


|<span data-ttu-id="177fe-272">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="177fe-272">**Example**</span></span>|<span data-ttu-id="177fe-273">**Verwendet für**</span><span class="sxs-lookup"><span data-stu-id="177fe-273">**Used for**</span></span>|<span data-ttu-id="177fe-274">**Format**</span><span class="sxs-lookup"><span data-stu-id="177fe-274">**Style**</span></span>|
|:-----|:-----|:-----|
|![Dateien ziehen](../images/AppUXGuidelines_dragfiles.png)|<span data-ttu-id="177fe-276">Inline-Haupttext am Anfang eines Parts.</span><span class="sxs-lookup"><span data-stu-id="177fe-276">Main inline text at the top of a part.</span></span>|<span data-ttu-id="177fe-277">.ms-textXLarge + .ms-soften</span><span class="sxs-lookup"><span data-stu-id="177fe-277">.ms-textXLarge + .ms-soften</span></span>|
|![ms-herocommandlink](../images/AppUXGuidelines_ms-herocommandlink.png)|<span data-ttu-id="177fe-279">Befehle in der obersten Zeile eines Parts; pro Part sollten maximal ein oder zwei enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="177fe-279">Commands in the top line of a part; at most there should be only one or two of these per part.</span></span>|<span data-ttu-id="177fe-280">.ms-heroCommandLink</span><span class="sxs-lookup"><span data-stu-id="177fe-280">.ms-heroCommandLink</span></span>|
|![ms-attractmode](../images/AppUXGuidelines_ms-attractmode.png)|<span data-ttu-id="177fe-282">Text, der angezeigt wird, um dem Benutzer einen Anreiz zur Interaktion mit dem Part zu geben, wenn dieser keine Daten enthält.</span><span class="sxs-lookup"><span data-stu-id="177fe-282">Text shown to entice the user to interact with the part when it doesn't contain data.</span></span>|<span data-ttu-id="177fe-283">.ms-attractMode</span><span class="sxs-lookup"><span data-stu-id="177fe-283">.ms-attractMode</span></span>|
|![ms-emptymode](../images/AppUXGuidelines_ms-emptymode.png)|<span data-ttu-id="177fe-285">Text, der für den Benutzer angezeigt wird, wenn keine Daten verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="177fe-285">Text shown to the user when there is no data available.</span></span>|<span data-ttu-id="177fe-286">.ms-emptyMode</span><span class="sxs-lookup"><span data-stu-id="177fe-286">.ms-emptyMode</span></span>|
|![mspivotlink](../images/AppUXGuidelines_mspivotlink.png)|<span data-ttu-id="177fe-288">Ansicht-Steuerelemente, wie z. B. ein Pivot-Element.</span><span class="sxs-lookup"><span data-stu-id="177fe-288">View controls, such as a pivot.</span></span>|<span data-ttu-id="177fe-289">.ms-pivot-link</span><span class="sxs-lookup"><span data-stu-id="177fe-289">.ms-pivot-link</span></span>|
|![ms-listlink](../images/AppUXGuidelines_ms-listlink.png)|<span data-ttu-id="177fe-291">Listenelemente, die auch Links sind.</span><span class="sxs-lookup"><span data-stu-id="177fe-291">List items that are also links.</span></span>|<span data-ttu-id="177fe-292">.ms-listLink</span><span class="sxs-lookup"><span data-stu-id="177fe-292">.ms-listLink</span></span>|

<span data-ttu-id="177fe-293">**Tabelle 7. Hintergrund- und Rahmenformatvorlagen**</span><span class="sxs-lookup"><span data-stu-id="177fe-293">**Table 7. Background and border styles**</span></span>


|<span data-ttu-id="177fe-294">**Beispiel**</span><span class="sxs-lookup"><span data-stu-id="177fe-294">**Example**</span></span>|<span data-ttu-id="177fe-295">**Verwendet für**</span><span class="sxs-lookup"><span data-stu-id="177fe-295">**Used for**</span></span>|<span data-ttu-id="177fe-296">**Format**</span><span class="sxs-lookup"><span data-stu-id="177fe-296">**Style**</span></span>|
|:-----|:-----|:-----|
|![ms-emphasis](../images/AppUXGuidelines_ms-emphasis.png)|<span data-ttu-id="177fe-298">Zum Formatieren eines Rechtecks, das auf der Seite stark hervorgehoben werden soll.</span><span class="sxs-lookup"><span data-stu-id="177fe-298">To style a rectangle that should be heavily emphasized on the page.</span></span>|<span data-ttu-id="177fe-299">.ms-emphasis</span><span class="sxs-lookup"><span data-stu-id="177fe-299">.ms-emphasis</span></span>|
|![ms-emphasisborder](../images/AppUXGuidelines_ms-emphasisborder.png)|<span data-ttu-id="177fe-301">Rahmen zum Hervorheben eines Elements.</span><span class="sxs-lookup"><span data-stu-id="177fe-301">Border of an emphasized element.</span></span>|<span data-ttu-id="177fe-302">.ms-emphasisBorder</span><span class="sxs-lookup"><span data-stu-id="177fe-302">.ms-emphasisBorder</span></span>|
|![ms-subtleemphasis](../images/AppUXGuidelines_ms-subtleemphasis.png)|<span data-ttu-id="177fe-304">Eine schwächere Hervorhebung eines Elements.</span><span class="sxs-lookup"><span data-stu-id="177fe-304">A more subtle emphasis of an element.</span></span>|<span data-ttu-id="177fe-305">.ms-subtleEmphasis</span><span class="sxs-lookup"><span data-stu-id="177fe-305">.ms-subtleEmphasis</span></span>|
|![ms-subtleemphasiscommand](../images/AppUXGuidelines_ms-subtleemphasiscommand.png)|<span data-ttu-id="177fe-307">Befehle in einem Element, mit ms-subtleEmphasis formatiert.</span><span class="sxs-lookup"><span data-stu-id="177fe-307">Commands in an element styled with ms-subtleEmphasis.</span></span>|<span data-ttu-id="177fe-308">.ms-subtleEmphasisCommand</span><span class="sxs-lookup"><span data-stu-id="177fe-308">.ms-subtleEmphasisCommand</span></span>|
|![ms-subtleemphasiscommand-disabled](../images/AppUXGuidelines_ms-subtleemphasiscommand-disabled.png)|<span data-ttu-id="177fe-310">Deaktivierter Befehl in einem Element, mit ms-subtleEmphasis formatiert.</span><span class="sxs-lookup"><span data-stu-id="177fe-310">Disabled command in an element styled with ms-subtleEmphasis.</span></span>|<span data-ttu-id="177fe-311">.ms-subtleEmphasisCommand-disabled</span><span class="sxs-lookup"><span data-stu-id="177fe-311">.ms-subtleEmphasisCommand-disabled</span></span>|
|![ms-sidenav](../images/AppUXGuidelines_ms-sidenav.png)|<span data-ttu-id="177fe-313">Seitliche Navigationselemente.</span><span class="sxs-lookup"><span data-stu-id="177fe-313">Side navigation elements.</span></span>|<span data-ttu-id="177fe-314">.ms-sideNav</span><span class="sxs-lookup"><span data-stu-id="177fe-314">.ms-sideNav</span></span>|
|![ms-sidenav-selected](../images/AppUXGuidelines_ms-sidenav-selected.png)|<span data-ttu-id="177fe-316">Zum Formatieren des ausgewählten seitlichen Navigationselements.</span><span class="sxs-lookup"><span data-stu-id="177fe-316">To style the selected side navigation element.</span></span>|<span data-ttu-id="177fe-317">.ms-sideNav-selected</span><span class="sxs-lookup"><span data-stu-id="177fe-317">.ms-sideNav-selected</span></span>|
|![ms-lines](../images/AppUXGuidelines_ms-lines.png)|<span data-ttu-id="177fe-319">Zum Hervorheben eines Elements durch einen Rahmen.</span><span class="sxs-lookup"><span data-stu-id="177fe-319">To emphasize an element using a border.</span></span>|<span data-ttu-id="177fe-320">.ms-lines</span><span class="sxs-lookup"><span data-stu-id="177fe-320">.ms-lines</span></span>|
|![ms-subtlelines](../images/AppUXGuidelines_ms-subtlelines.png)|<span data-ttu-id="177fe-322">Zum Hervorheben eines Elements durch einen feinen Rahmen.</span><span class="sxs-lookup"><span data-stu-id="177fe-322">To emphasize an element using a subtle border.</span></span>|<span data-ttu-id="177fe-323">.ms-subtleLines</span><span class="sxs-lookup"><span data-stu-id="177fe-323">.ms-subtleLines</span></span>|
|![ms-stronglines](../images/AppUXGuidelines_ms-stronglines.png)|<span data-ttu-id="177fe-325">Zum Hervorheben eines Elements durch einen starken oder farbigen Rahmen.</span><span class="sxs-lookup"><span data-stu-id="177fe-325">To emphasize an element using a strong or colored border.</span></span>|<span data-ttu-id="177fe-326">.ms-strongLines</span><span class="sxs-lookup"><span data-stu-id="177fe-326">.ms-strongLines</span></span>|
|![ms-disabledlines](../images/AppUXGuidelines_ms-disabledlines.png)|<span data-ttu-id="177fe-328">Zum Hervorheben eines deaktivierten Elements durch einen Rahmen.</span><span class="sxs-lookup"><span data-stu-id="177fe-328">To emphasize a disabled element using a border.</span></span>|<span data-ttu-id="177fe-329">.ms-disabledLines</span><span class="sxs-lookup"><span data-stu-id="177fe-329">.ms-disabledLines</span></span>|
|![ms-accentlines](../images/AppUXGuidelines_ms-accentlines.png)|<span data-ttu-id="177fe-331">Zum Hervorheben eines Elements durch einen Akzentuierungsrahmen.</span><span class="sxs-lookup"><span data-stu-id="177fe-331">To emphasize an element using an accent border.</span></span>|<span data-ttu-id="177fe-332">.ms-accentLines</span><span class="sxs-lookup"><span data-stu-id="177fe-332">.ms-accentLines</span></span>|
|![ms-popupborder](../images/AppUXGuidelines_ms-popupborder.png)|<span data-ttu-id="177fe-334">Zum Begrenzen eines Popupfensters.</span><span class="sxs-lookup"><span data-stu-id="177fe-334">To contain pop-up windows.</span></span>|<span data-ttu-id="177fe-335">.ms-popupBorder</span><span class="sxs-lookup"><span data-stu-id="177fe-335">.ms-popupBorder</span></span>|
|![ms-bgoverlay](../images/AppUXGuidelines_ms-bgoverlay.png)|<span data-ttu-id="177fe-337">Zum Anwenden einer Überlagerung auf das Hintergrundelement.</span><span class="sxs-lookup"><span data-stu-id="177fe-337">To apply an overlay on the background element.</span></span>|<span data-ttu-id="177fe-338">.ms-bgOverlay</span><span class="sxs-lookup"><span data-stu-id="177fe-338">.ms-bgOverlay</span></span>|
|![bgdisabled](../images/AppUXGuidelines_bgdisabled.png)|<span data-ttu-id="177fe-340">Um den Hintergrund eines Elements deaktiviert erscheinen zu lassen.</span><span class="sxs-lookup"><span data-stu-id="177fe-340">To make the background of an element appear disabled.</span></span>|<span data-ttu-id="177fe-341">.ms-bgDisabled</span><span class="sxs-lookup"><span data-stu-id="177fe-341">.ms-bgDisabled</span></span>|
|![ms-bgheader](../images/AppUXGuidelines_ms-bgheader.png)|<span data-ttu-id="177fe-343">Zum Anwenden der Kopfzeilen-Hintergrundfarbe.</span><span class="sxs-lookup"><span data-stu-id="177fe-343">To apply the header background color.</span></span>|<span data-ttu-id="177fe-344">.ms-bgHeader</span><span class="sxs-lookup"><span data-stu-id="177fe-344">.ms-bgHeader</span></span>|
|![ms-bgfooter](../images/AppUXGuidelines_ms-bgfooter.png)|<span data-ttu-id="177fe-346">Zum Anwenden der Fußzeilen-Hintergrundfarbe.</span><span class="sxs-lookup"><span data-stu-id="177fe-346">To apply the footer background color.</span></span>|<span data-ttu-id="177fe-347">.ms-bgFooter</span><span class="sxs-lookup"><span data-stu-id="177fe-347">.ms-bgFooter</span></span>|
|![md-bghoverable normal](../images/AppUXGuidelines_md-bghoverable-normal.png)|<span data-ttu-id="177fe-p117">Elemente, die farblich hervorgehoben werden sollen, wenn mit dem Mauszeiger darauf gezeigt wird. Das Beispiel zeigt das Element, wenn nicht mit dem Mauszeiger darauf gezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="177fe-p117">Elements that should have a highlighted color on hover. The example shows the element when the mouse is not hovering over it.</span></span>|<span data-ttu-id="177fe-351">.ms-bgHoverable</span><span class="sxs-lookup"><span data-stu-id="177fe-351">.ms-bgHoverable</span></span>|
|![ms-bghoverable-onhover](../images/AppUXGuidelines_ms-bghoverable-onhover.png)|<span data-ttu-id="177fe-p118">Elemente, die farblich hervorgehoben werden sollen, wenn mit dem Mauszeiger darauf gezeigt wird. Das Beispiel zeigt das Element, wenn mit dem Mauszeiger darauf gezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="177fe-p118">Elements that should have a highlighted color on hover. The example shows the element when the mouse is hovering over it.</span></span>|<span data-ttu-id="177fe-355">.ms-bgHoverable</span><span class="sxs-lookup"><span data-stu-id="177fe-355">.ms-bgHoverable</span></span>|
|![ms-bgselected](../images/AppUXGuidelines_ms-bgselected.png)|<span data-ttu-id="177fe-357">Zum Anzeigen der Auswahl eines Elements.</span><span class="sxs-lookup"><span data-stu-id="177fe-357">To show selection on an element.</span></span>|<span data-ttu-id="177fe-358">.ms-bgSelected</span><span class="sxs-lookup"><span data-stu-id="177fe-358">.ms-bgSelected</span></span>|
|![ms-topbar](../images/AppUXGuidelines_ms-topbar.png)|<span data-ttu-id="177fe-360">Elemente in der obersten Leiste der Seite.</span><span class="sxs-lookup"><span data-stu-id="177fe-360">Elements in the top bar of the page.</span></span>|<span data-ttu-id="177fe-361">.ms-topBar</span><span class="sxs-lookup"><span data-stu-id="177fe-361">.ms-topBar</span></span>|
<span data-ttu-id="177fe-362">Weitere Informationen finden Sie unter [Verwenden einer SharePoint-Formatvorlage in SharePoint Add-Ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="177fe-362">For more information, see  [Use a SharePoint website's style sheet in SharePoint Add-ins](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md).</span></span>
 

 

## <a name="styling-common-items-consistently-in-sharepoint-add-ins"></a><span data-ttu-id="177fe-363">Einheitliches Formatieren häufiger Elemente in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-363">Styling common items consistently in SharePoint Add-ins</span></span>
<span data-ttu-id="177fe-364"><a name="UXGuide_Styling"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-364"><a name="UXGuide_Styling"> </a></span></span>

<span data-ttu-id="177fe-365">Damit Benutzer sich Fertigkeiten aneignen können, die sowohl in SharePoint als auch in Add-Ins anwendbar sind, sollten Sie gemeinsame Elemente konsistent formatieren.</span><span class="sxs-lookup"><span data-stu-id="177fe-365">To help users learn skills that translate between SharePoint and add-ins, you should style several common elements consistently.</span></span>
 

 

### <a name="internal-navigation"></a><span data-ttu-id="177fe-366">Interne Navigation</span><span class="sxs-lookup"><span data-stu-id="177fe-366">Internal navigation</span></span>

<span data-ttu-id="177fe-p119">Um die Navigation innerhalb Ihres Add-Ins zu ermöglichen, stehen hauptsächlich zwei Konzepte zur Verfügung: Linksnavigation und Topnavigation. Für welche Option Sie sich entscheiden, hängt in gewissem Maße auch vom weiteren Inhalt in Ihres Add-Ins ab. In der Regel ist Linksnavigation die richtige Wahl, insbesondere wenn Sie zwischen verschiedenen Listen umschalten oder der Fokus Ihres Add-Ins eine Master-Detail-Ansicht ist. Wenn andererseits Ihre Navigation hauptsächlich zwischen Ansichten wechselt, die als verschiedene Ansichten einer Liste betrachtet werden können, könnten Sie statt dessen auch Topnavigation wählen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p119">To provide navigation within your add-in, there are two main patterns to follow: left navigation and top navigation. Which option you use depends somewhat on what the content is in the rest of your add-in. In general, left navigation will be the correct choice, particularly if you're switching between different lists, or the focus of your add-in is a master-detail view. On the other hand, if your navigation mainly switches between what could be considered different views of the same list, you could choose to use top navigation instead.</span></span>
 

 
<span data-ttu-id="177fe-p120">Sowohl die Linksnavigation als auch die Topnavigation verfügen über Objektmodelldarstellungen, die korrekt formatiert werden, wenn sie in SharePoint festgelegt werden. Außerhalb von SharePoint-Seiten ist etwas mehr Aufwand erforderlich, um das Markup für die Top- oder die Linksnavigation selbst zu erstellen und dann die entsprechenden CSS-Klasses für die korrekte Formatierung hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p120">Both left navigation and top navigation have object model representations that will be styled correctly when they are set in SharePoint. Outside of SharePoint pages, you'll have to do a bit more work to create the markup for the top or left navigation yourself, and then add the appropriate CSS classes so that it's styled correctly.</span></span>
 

 

### <a name="toolbars"></a><span data-ttu-id="177fe-373">Symbolleisten</span><span class="sxs-lookup"><span data-stu-id="177fe-373">Toolbars</span></span>

<span data-ttu-id="177fe-p121">In vielen Fällen verfügen Sie über eine kleine Anzahl von Befehlen, die Sie für Ihre Benutzer schnell verfügbar machen möchten. Wenn Sie das Menüband bereits auf Ihrer Seite verwenden, empfiehlt es sich, diese Befehle an logischen Positionen dem vorhandenen Menüband hinzuzufügen. Falls Sie jedoch auf der Seite noch über kein Menüband verfügen, ist es wahrscheinlich nicht sinnvoll, nur wegen ein paar Befehlen ein Menüband hinzuzufügen. In diesem Fall wird empfohlen, eine Symbolleiste hinzuzufügen, die auf das Element kontextbezogen ist, für das die Befehle gelten sollen. Verwenden Sie dazu Glyphe, mit ms-commandLink formatierten Text oder beides, um Ihre Befehle in der Symbolleiste dazustellen, welche die gleiche Hintergrundfarbe haben sollte wie die restliche Seite.</span><span class="sxs-lookup"><span data-stu-id="177fe-p121">In many cases, you will have a small number of commands that you want to surface quickly to the user. If you are using the ribbon on your page already, the best choice is to add those commands to logical locations within the existing ribbon. However, in the case where you don't already have a ribbon on the page, it probably doesn't make sense to add one for a handful of commands. In that case, we recommend that you add a toolbar contextual to the item where the commands will apply. You should use either glyph, text styled with ms-commandLink, or both, to represent your commands on the toolbar, which should have the same background color as the rest of the page.</span></span>
 

 

### <a name="lists"></a><span data-ttu-id="177fe-379">Listen</span><span class="sxs-lookup"><span data-stu-id="177fe-379">Lists</span></span>

<span data-ttu-id="177fe-p122">Listen sind eine gängige Möglichkeit zur Darstellung von Daten für Benutzer. Wenn Ihr Add-In SharePoint-Seiten verwendet, können Sie das Listenansicht-Webpart verwenden, um Daten für Benutzer darzustellen und über die damit verbundenen Formatierungs- und Interaktionsmöglichkeiten zu verfügen. Wenn sich Ihre Seiten jedoch an anderer Stelle befinden oder Sie die Interaktion von Benutzern mit Ihrer Liste stärker steuern möchten, sollten Sie die Listenformatierung in SharePoint imitieren, während Sie Ihre eigenen Rendering- und Interaktionsmöglichkeiten bereitstellen. Nachfolgend sind einige Formatierungsprobleme aufgeführt, die Sie bei der Verwendung von Listen in Ihrem Add-In berücksichtigen sollten:</span><span class="sxs-lookup"><span data-stu-id="177fe-p122">Lists are a common way to represent data to users. If your add-in is using SharePoint pages, you could use the List View Web Part to represent the data to users and get the styling and interaction that comes with it. However, if you have your pages elsewhere, or you want more control over the interaction that users have with your list, you should mimic the styling of lists in SharePoint while providing your own rendering and interaction. The following are some style issues to keep in mind when you are using lists in your add-in:</span></span>
 

 

-  <span data-ttu-id="177fe-p123">**Ansichten:** Wenn Sie mehrere Ansichten in einer einzelnen Liste darstellen, sollten Sie am Anfang der Liste ein Pivot-Element verwenden, wie dies bei regulären SharePoint-Listen der Fall ist. Verwenden Sie jedoch niemals Pivot-Elemente für die Darstellung von Master-Detail-Daten.</span><span class="sxs-lookup"><span data-stu-id="177fe-p123">**Views:** When representing multiple views on a single list, you should use a pivot at the top of the list, just as regular SharePoint lists do. You should never use pivots as a way of representing master-detail data.</span></span>
    
 
-  <span data-ttu-id="177fe-p124">**Filter:** Wenn Sie einen Filter für eine bestehende Liste oder eine Master-Detail-Anordnung bereitstellen, verwenden Sie eine Randleiste, die bündig mit der linken Seite des Inhaltsbereichs abschließt und eine Breite von mindestens 300 Pixel hat. Kopieren Sie außerdem die SharePoint-Auswahlformatierung, um für den Benutzer anzugeben, welche Filter oder Elemente ausgewählt wurden.</span><span class="sxs-lookup"><span data-stu-id="177fe-p124">**Filters:** When providing a filter on an existing list or a master-detail arrangement, you should use a sidebar that is flush with the left side of the content area and that is at least 300-pixels wide. You should also copy the SharePoint selection styling to indicate to the user which filters or items are selected.</span></span>
    
 
-  <span data-ttu-id="177fe-388">**Formulare:** Wenn ein Benutzer ein einzelnes Element anzeigt oder bearbeitet, sollten Sie entweder die integrierten SharePoint-Formulare verwenden oder ihre Formatierung imitieren, um eine konsistente Nutzungserfahrung zu vermitteln.</span><span class="sxs-lookup"><span data-stu-id="177fe-388">**Forms:** When a user is viewing or editing a single item, you should either use the built-in SharePoint forms or mimic their styling for a consistent experience.</span></span>
    
 

### <a name="forms-dialog-boxes-and-callouts"></a><span data-ttu-id="177fe-389">Formulare, Dialogfelder und Legenden</span><span class="sxs-lookup"><span data-stu-id="177fe-389">Forms, dialog boxes, and callouts</span></span>

<span data-ttu-id="177fe-p125">Es gibt drei verschiedene Möglichkeiten, um für Benutzer Informationen über ein Objekt bereitzustellen oder um eine Benutzeroberfläche (UI) für die Benutzereingabe zu bieten: Ganzseitige Formulare, Dialogfelder und Legenden. Welche Option Sie wählen, hängt von der Benutzerintention sowie davon ab, wie viele Informationen angezeigt oder abgefragt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p125">There are three distinct patterns for providing the user with more information about an object, or for providing a user interface (UI) for user input: full-page forms, dialog boxes, and callouts. Whichever one you use depends on the user intent and how much information will be shown or requested.</span></span>
 

 

-  <span data-ttu-id="177fe-p126">**Ganzseitige Formulare:** Dies ist die beste Option, wenn Benutzer mehrere unterschiedliche Informationen eingeben sollen, oder wenn viele strukturierte Informationen gleichzeitig für sie angezeigt werden sollen. Ganzseitige Formulare sind auch in Szenarien am sinnvollsten, in denen komplexere Interaktionsmodelle erforderlich sind , wie z. B. das Menüband. In diesem Fall verweisen Sie den Benutzer bei Bedarf auf die Formularseite. Stellen Sie sicher, dass Benutzer über eine einfache Möglichkeit zum Speichern oder Verwerfen ihrer Änderungen verfügen, entweder mithilfe von Schaltflächen oder mit dem Menüband. In sehr langen Formularen, in denen Bildläufe durchgeführt werden müssen, empfiehlt es sich, die Optionen **Speichern** und **Abbrechen** sowohl am oberen als auch am unteren Rand des Formulars zu positionieren.</span><span class="sxs-lookup"><span data-stu-id="177fe-p126">**Full-page forms:** This is the best choice when you want users to enter several different pieces of information, or you want to show them a lot of structured information at one time. Full-page forms also make the most sense in scenarios where more complex interaction models, such as the ribbon, are required. In this case, you would point the user to the form page when necessary. You should make sure that there is a clear way to save or cancel their changes, by using either buttons or the ribbon. In very long forms that might require scrolling, it's a good idea to place the **Save** and **Cancel** options at both the top and bottom of the form.</span></span>
    
 
-  <span data-ttu-id="177fe-p127">**Dialogfelder:** Dies sind modale Benutzeroberflächen-Container, die in der Regel verwendet werden, um weitere Informationen oder Aktionen auf kontextbezogene Weise anzuzeigen. Sie werden auch für kürzere Formulare oder Benutzereingaben verwendet. In der Regel sollte die in einem Dialogfeld gehostete Benutzeroberfläche einfach und für eine kleinere Rendering-Oberfläche gut geeignet sein. Für längere Formulare oder komplexere Interaktionsmodelle, wie z. B. das Menüband, empfiehlt sich dagegen die Verwendung ganzseitiger Formulare.</span><span class="sxs-lookup"><span data-stu-id="177fe-p127">**Dialog boxes:** These are modal UI containers that are typically used to show more information or actions in a contextual manner. They are also used for shorter forms or user input. In general, the UI that is hosted within a dialog box should be simple and well suited for a smaller rendering surface. Longer forms or more complex interaction models, such as the ribbon, are better served by full-page forms instead.</span></span>
    
 
-  <span data-ttu-id="177fe-p128">**Legenden:** Diese geben wichtige kontextbezogene Informationen und Aktionen zu einem bestimmten Element an. Legenden werden in der Regel verwendet, um dem Benutzer in einer kleinen Benutzeroberfläche weitere Informationen oder Aktionen zu einem Element anzugeben. Wenn Bildlaufleisten oder Benutzereingaben erforderlich sind, ist die Legende möglicherweise keine gute Wahl.</span><span class="sxs-lookup"><span data-stu-id="177fe-p128">**Callouts:** These provide relevant contextual information and actions around a particular item. Callouts are generally used to show the user more information or actions about an item in a lightweight UI. If scrollbars or user input are necessary, the callout is probably not a good choice.</span></span>
    
 

### <a name="animation"></a><span data-ttu-id="177fe-404">Animation</span><span class="sxs-lookup"><span data-stu-id="177fe-404">Animation</span></span>

<span data-ttu-id="177fe-p129">Animation kann zwar zu einer lebendigeren und interessanteren Benutzeroberfläche führen, Sie sollten jedoch eine übermäßige Verwendung in Ihrer Benutzeroberfläche vermeiden. Gut gemachte Animation wird vom Benutzer kaum bewusst wahrgenommen, sondern vermittelt ihm den Eindruck einer schnelleren, leistungsfähigeren Benutzeroberfläche. Sie sollten bei der Anwendung von Animation unbedingt Konzepte wie Bewegung und Trägheit berücksichtigen und eine Benutzeroberfläche bereitstellen, die natürlich und ansprechend wirkt. Es wird nachdrücklich davon abgeraten, übertriebenen Animationen zu verwenden, wie z. B. übermäßiges Prellen oder Federn oder das Umherfliegen von Objekten auf dem Bildschirm bei der kleinsten Benutzeraktion. Objekte sollten generell auf dem direkten Weg zu ihrem Ziel gelangen und beanspruchen häufig nur die ersten oder letzten zehn Prozent der tatsächlichen Änderung durch die Animation, mit der dem Benutzer der Eindruck einer Bewegung vermittelt werden soll.</span><span class="sxs-lookup"><span data-stu-id="177fe-p129">Although animation can lead to a more vibrant and engaging experience, you should be careful to not overuse it in your UI. Animation that is done well will be hardly noticeable by the user, but it will give the impression of faster, better-performing UI. When using animation, you should make sure to respect concepts like physics and inertia and provide UI that seems natural and graceful. We strongly recommend against exaggerated animations like excessive bouncing or elasticity, or having objects fly around the screen at the slightest user action. Objects should generally take a direct path to their destination, and often will only need the first or last 10 percent of the actual change to be animated in order to give the user the sense that it has moved.</span></span>
 

 

### <a name="tabs-and-pivots"></a><span data-ttu-id="177fe-410">Registerkarten und Pivot-Elemente</span><span class="sxs-lookup"><span data-stu-id="177fe-410">Tabs and pivots</span></span>

<span data-ttu-id="177fe-p130">Das Menüband ist der einzige Ort in SharePoint, an dem Sie Registerkarten verwenden sollten. An jedem anderen Ort in SharePoint sollten Sie mithilfe von Pivot-Elementen das Konzept der Änderung des Inhaltsbereichs ausdrücken.</span><span class="sxs-lookup"><span data-stu-id="177fe-p130">In SharePoint, the only place where you should use tabs is on the ribbon. Everywhere else in SharePoint should use pivots to express the concept of changing the content area.</span></span>
 

 

## <a name="office-ui-fabric-with-sharepoint-add-ins-faq"></a><span data-ttu-id="177fe-413">Häufig gestellte Fragen zu Office UI Fabric mit SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-413">Office UI Fabric with SharePoint Add-ins FAQ</span></span>
<span data-ttu-id="177fe-414"><a name="Fabric"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-414"><a name="Fabric"> </a></span></span>

<span data-ttu-id="177fe-415">Verwenden Sie diese häufig gestellten Fragen, um zu verstehen, wie Sie Office UI Fabric verwenden und Ihre SharePoint-Add-In wie das restliche Office 365 aussehen und sich verhalten lassen.</span><span class="sxs-lookup"><span data-stu-id="177fe-415">Use this FAQ to understand how to use Office UI Fabric and make your SharePoint Add-in look and feel like the rest of the Office 365.</span></span>
 

 
 <span data-ttu-id="177fe-416">**1. Was ist Office UI Fabric?**</span><span class="sxs-lookup"><span data-stu-id="177fe-416">**1. What is Office UI Fabric?**</span></span>
 

 
<span data-ttu-id="177fe-p131">Office UI Fabric ist ein reaktionsfähiges, mobilorientiertes Front-End-Framework, mit dem Sie Webbenutzeroberflächen über die Office-Entwurfssprache erstellen können. Das Tool wird mit einem Schriftartensatz und CSS-Klassen implementiert, die Benutzeroberflächenkomponenten, Symbole, Animation und die offizielle Office-Farbpalette bereitstellen. Ausführliche Informationen finden Sie unter  [Office UI Fabric](https://github.com/OfficeDev/Office-UI-Fabric).</span><span class="sxs-lookup"><span data-stu-id="177fe-p131">Office UI Fabric is a responsive, mobile-first, front-end framework that enables you to create web experiences by using the Office Design Language. It is implemented with a set of fonts and with CSS classes that provide UI components, icons, animation, and the official Office color palette. For details, see  [Office UI Fabric](https://github.com/OfficeDev/Office-UI-Fabric).</span></span>
 

 
 <span data-ttu-id="177fe-420">**2. Kann ich Office UI Fabric in meinen SharePoint-Add-Ins verwenden?**</span><span class="sxs-lookup"><span data-stu-id="177fe-420">**2. Can I use Office UI Fabric in my SharePoint Add-ins?**</span></span>
 

 
<span data-ttu-id="177fe-p132">Ja. Ihre Add-In-Seiten können auf dieselbe Weise auf Office UI Fabric-Dateien verweisen, wie auf andere CSS-Frameworks wie Bootstrap verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="177fe-p132">Yes. Your add-in pages can reference the Office UI Fabric files in the same way that other CSS frameworks, like bootstrap, are referenced.</span></span>
 

 
 <span data-ttu-id="177fe-423">**3. Wann sollte ich Office UI Fabric mit SharePoint-Add-Ins verwenden?**</span><span class="sxs-lookup"><span data-stu-id="177fe-423">**3. When should I use Office UI Fabric with SharePoint Add-ins?**</span></span>
 

 
<span data-ttu-id="177fe-p133">Verwenden Sie das Tool, wenn Sie Ihrem Add-In das Aussehen und Verhalten von Office 365 geben möchten. Es ist eine Alternative zur Verwendung der CSS-Datei des SharePoint-Hostwebs.</span><span class="sxs-lookup"><span data-stu-id="177fe-p133">Use it when you want your add-in to have the look and feel of Office 365. It is an alternative to using the CSS file of the SharePoint host web.</span></span>
 

 
 <span data-ttu-id="177fe-426">**4. Wie kann Office UI Fabric in SharePoint-Add-Ins verwendet werden?**</span><span class="sxs-lookup"><span data-stu-id="177fe-426">**4. How can Office UI Fabric be used in SharePoint Add-ins?**</span></span>
 

 
<span data-ttu-id="177fe-p134">Fügen Sie einfach die Office UI Fabric-Dateien zu Ihrem Entwicklungsprojekt hinzu, und schließen Sie einen Verweis zur fabric.css-Bibliothek in Ihre HTML- oder ASPX-Seite ein. Ausführliche Informationen finden Sie unter  [Erste Schritte](https://github.com/OfficeDev/Office-UI-Fabric#get-started).</span><span class="sxs-lookup"><span data-stu-id="177fe-p134">Just add the Office UI Fabric files to your development project, and include a reference to the fabric.css library to your HTML or ASPX page. For details, see  [Getting started](https://github.com/OfficeDev/Office-UI-Fabric#get-started).</span></span>
 

 
 <span data-ttu-id="177fe-429">**5. Wie können Office UI Fabric-Komponenten in SharePoint-Add-Ins verwendet werden?**</span><span class="sxs-lookup"><span data-stu-id="177fe-429">**5. How can Office UI Fabric Components be used in SharePoint Add-ins?**</span></span>
 

 
<span data-ttu-id="177fe-p135">Fügen Sie einfach einen Verweis auf die fabric.components.css-Bibliothek zu Ihrer HTML- oder ASPX-Seite hinzu. Ausführliche Informationen finden Sie unter [Erste Schritte](https://github.com/OfficeDev/Office-UI-Fabric/blob/master/ghdocs/GETTINGSTARTED).</span><span class="sxs-lookup"><span data-stu-id="177fe-p135">Just add a reference to the fabric.components.css library to your HTML or ASPX page. For details, see  [Getting started](https://github.com/OfficeDev/Office-UI-Fabric/blob/master/ghdocs/GETTINGSTARTED).</span></span>
 

 
 <span data-ttu-id="177fe-432">**6. Kann ich Office UI Fabric zusammen mit einer Hostweb-CSS-Datei eines SharePoint-Add-Ins verwenden?**</span><span class="sxs-lookup"><span data-stu-id="177fe-432">**6. Can I use Office UI Fabric along with a SharePoint Add-in's host web CSS?**</span></span>
 

 
<span data-ttu-id="177fe-p136">Derzeit raten wir davon ab, Office UI Fabric mit Hostweb-CSS zu mischen. Damit sollen Konflikte bei Klassennamen und Formatvorlagen vermieden werden.</span><span class="sxs-lookup"><span data-stu-id="177fe-p136">Currently, we recommend against mixing Office UI Fabric with host web CSS. This is to prevent class name collisions and style mismatches.</span></span>
 

 
 <span data-ttu-id="177fe-435">**7. Unterstützt Office UI Fabric SharePoint-Designs?**</span><span class="sxs-lookup"><span data-stu-id="177fe-435">**7. Does Office UI Fabric support SharePoint themes?**</span></span>
 

 
<span data-ttu-id="177fe-p137">Nein. Office UI Fabric bietet keine Unterstützung für SharePoint-Designs. Das Anwenden von Office UI Fabric-Designs führt jedoch nicht zu Konflikten mit SharePoint-Designs.</span><span class="sxs-lookup"><span data-stu-id="177fe-p137">No. Office UI Fabric does not support SharePoint themes. However, applying Office UI Fabric theming will not conflict with SharePoint themes.</span></span>
 

 

## <a name="extending-sharepoint-ui-in-add-ins"></a><span data-ttu-id="177fe-439">Erweitern der SharePoint-Benutzeroberfläche in Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-439">Extending SharePoint UI in add-ins</span></span>
<span data-ttu-id="177fe-440"><a name="UXGuide_Extending"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-440"><a name="UXGuide_Extending"> </a></span></span>

<span data-ttu-id="177fe-p138">In SharePoint kann die bestehende Benutzeroberfläche durch Add-Ins erweitert werden. Dadurch können Sie Ihr Add-In dort bereitstellen, wo Benutzer es benötigen. Sie können die Benutzeroberfläche der Hostwebsite mit den folgenden Methoden erweitern:</span><span class="sxs-lookup"><span data-stu-id="177fe-p138">SharePoint allows add-ins to extend some of the existing UI, which enables you to make your add-in available in the places where users might need it. You can extend the host web's UI by using the following methods:</span></span>
 

 

-  <span data-ttu-id="177fe-443">**Add-In-Parts**: Ermöglichen Ihnen, ein **iframe**-Element bereitzustellen, das Inhalt Ihres Add-Ins enthält.</span><span class="sxs-lookup"><span data-stu-id="177fe-443">**Add-in parts:** Enable you to surface an **iframe** element to contain content from your add-in.</span></span>
    
 
-  <span data-ttu-id="177fe-p139">**Benutzerdefinierte Aktionen:** Sie können das Menüband oder das Kontextmenü durch benutzerdefinierte Aktionen erweitern. Benutzerdefinierte Aktionen machen Ihr Add-In in Listenelementen oder Dokumenten verfügbar, oder überall dort, wo das Menüband angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="177fe-p139">**Custom actions:** You can extend the ribbon or contextual menu through custom actions. Custom actions make your add-in available on list items or documents, or anywhere else the ribbon is shown.</span></span>
    
 

### <a name="adding-add-in-parts-to-the-host-web"></a><span data-ttu-id="177fe-446">Hinzufügen von Add-In-Parts zur Hostwebsite</span><span class="sxs-lookup"><span data-stu-id="177fe-446">Adding add-in parts to the host web</span></span>

<span data-ttu-id="177fe-p140">Parts bieten für Ihr Add-In eine Möglichkeit, Informationen oder einen kleinen Interaktionspunkt in der Hostwebsite, auf der das Add-In installiert ist, anzuzeigen. Endbenutzer können diese Parts in ihre Seiten integrieren, indem Sie das Webpartframework in SharePoint verwenden. Abbildung 3 zeigt das Part Tag-Cloud als Beispiel für ein Part.</span><span class="sxs-lookup"><span data-stu-id="177fe-p140">Parts are a way for your add-in to surface some information or a small interaction point in the host web where the add-in is installed. End users can embed those parts in their pages by using the Web Part framework in SharePoint. Figure 3 shows the tag cloud part as an example of a part.</span></span>
 

 

<span data-ttu-id="177fe-450">**Abbildung 3. Das Part Tag-Cloud**</span><span class="sxs-lookup"><span data-stu-id="177fe-450">**Figure 3. Tag cloud part**</span></span>

 

 
![Das Part Tag-Cloud](../images/AppUXGuidelines_part.png)
 
<span data-ttu-id="177fe-p141">Der Titel des Parts in Abbildung 3 ist **Tag-Cloud aus Add-In UX Design**. Die Tag-Cloud selbst wird vom Add-In-Inhalt bereitgestellt. Sie ist in einem **iframe**-Element gehostet und von der Hostingseite vollständig isoliert. Da der Add-In-Inhalt die CSS-Datei der Hostwebsite verwendet, fügt sie sich nahtlos in die Hostseite ein.</span><span class="sxs-lookup"><span data-stu-id="177fe-p141">In Figure 3, the  **Tag Cloud from UX Design add-in** is the title of the part. The tag cloud itself is served from the add-in content, and it is hosted in an **iframe** element and fully isolated from the hosting page. Because the add-in content is using the host web's CSS file, it fits in seamlessly with the host page.</span></span>
 

 
<span data-ttu-id="177fe-p142">Einige Benutzeroberflächenarten eignen sich gut für die Bereitstellung durch Part-Benutzeroberflächen. Zum Beispiel möchten Sie vielleicht eine Gruppe von Tastenkombinationen in verschiedenen Bereichen Ihres Add-Ins bereitstellen, oder sogar einen einzelnen Startpunkt, den Benutzer in andere Seiten integrieren können. Eine weitere Möglichkeit wäre, einen kleinen Teilsatz der Daten im Add-In oder die neuesten Änderungen beliebiger Elemente anzuzeigen. Vielleicht möchten Sie eine kleine interaktive Zone bereitstellen, die die Durchführung von schnellen Aktionen mit dem Add-In ermöglicht, ohne dass es dazu geöffnet werden muss. Welchen Part-Typ Sie wählen, wird von den Szenarien bestimmt, die Ihr Add-In unterstützt. Bedenken Sie immer, dass nicht für alle Add-Ins Parts erforderlich sind. Stellen Sie Parts nur bereit, wenn sie für die Gesamtwirkung sinnvoll sind.</span><span class="sxs-lookup"><span data-stu-id="177fe-p142">Some kinds of UI lend themselves well to being exposed through part UI. For example, you might want to provide a set of shortcuts into different experiences of your add-in, or even a single launch point that users can embed on other pages. Another use might be to show a small subset of the data in the add-in, or show the most recent changes to something. You might want to provide a small interactive zone for performing quick actions with the add-in without having to open it to do so. What type of part you provide will be driven by the scenarios your add-in supports. You should keep in mind that not all add-ins will have parts, you should only provide them if they make sense for the user experience.</span></span>
 

 
<span data-ttu-id="177fe-p143">Die Seite, die Sie innerhalb des Parts anzeigen, wird in einem **iframe**-Element gehostet. Stellen Sie daher sicher, dass dies dem von Ihnen geschriebenen JavaScript bekannt ist und es auf Objekte, wie z. B. das Fensterobjekt, zugreifen kann. Selbst wenn der Rest Ihres Add-Ins durch ausgeprägtes Branding gekennzeichnet ist, sollten Sie in Betracht ziehen, für Ihr Part die Formate der Hostwebsite zu übernehmen. Denn dieses wird in die Seiten der Hostwebsite integriert und sieht weder harmonisch noch ansprechend aus, wenn es nicht dazu passt. Um die Formate der Hostwebsite zu übernehmen, müssen Sie den Link zur CSS-Standarddatei manuell erstellen. Weitere Informationen finden Sie unter  [Vorgehensweise: Verweisen auf die CSS-Datei der Hostwebsite](#UXGuide_CSS) in diesem Artikel. Auf der Seite darf sich auch kein Chromsteuerelement befinden, denn es wird in eine Seite integriert, die bereits über ein Chromsteuerelement verfügt.</span><span class="sxs-lookup"><span data-stu-id="177fe-p143">The page you display inside the part will be hosted in an  **iframe**, so you should make sure that any JavaScript you write is aware of that and is smart about accessing things like the window object. Even if the rest of your add-in is heavily branded, you should consider adopting the host web's styling for your part, because it will be embedded within the host web's pages and will look jarring and unappealing if it doesn't fit in. In order to use the host web's styling, you'll have to build the link to the default CSS file manually. For more information, see  [How to: Reference the host web's CSS file](#UXGuide_CSS) in this article. There also should not be any chrome on the page, because it will be embedded on a page that already has chrome itself.</span></span>
 

 
<span data-ttu-id="177fe-p144">Da die Seite in einem **iframe**-Element über verschiedene Domänen hinweg einwandfrei funktionieren soll, müssen Sie sicherstellen, dass Sie nicht „Same-Origin-Only“ für X-Frame-Optionen dieser Seite angeben. SharePoint-Seiten geben standardmäßig an, dass sie sich in einem **iframe**-Element innerhalb einer Domäne befinden müssen. Für Seiten, die in SharePoint gehostet werden, müssen Sie daher für die Seiten, die Sie in Parts anzeigen möchten, dieses Verhalten deaktivieren. Dazu fügen Sie an einer beliebigen Stelle auf der Seite das Webpart **AllowFraming** hinzu, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="177fe-p144">The page has to work nicely in an  **iframe** across different domains, so you'll have to make sure that you do not specify same-origin only for X-Framing-Options of this page. By default, SharePoint pages do specify that they should only be in an **iframe** within the same domain. So for pages that are hosted in SharePoint, you'll have to opt out of that behavior for the pages you want to show in parts by adding the **AllowFraming** Web Part somewhere on the page, as shown in the following example.</span></span>
 

 



```
<WebPartPages:AllowFraming ID="AllowFraming1" runat="server" />
```

<span data-ttu-id="177fe-p145">Da Sie nicht erzwingen können, in welche Domänen Ihre Seiten per iFrame gelangen, sind die von Ihnen in Add-In-Parts gehosteten Seiten anfällig für Sicherheitsangriffe durch Clickjacking, Seiten können sich in einem iFrame auf einer schädlichen Seite befinden, und Benutzer könnten dazu verleitet werden, auf Schaltflächen zu klicken und Aktionen durchzuführen, derer sie sich nicht bewusst sind. Wenn Sie Ihre Seite planen, sollten Sie dies berücksichtigen und sicherstellen, dass Sie auf der Seite für das Part keine Funktion exponieren, die gefährlich wäre, wenn sie auf einer schädlichen Seite angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="177fe-p145">Because you cannot enforce which domains your pages are iframed into, the pages you host in add-in parts are vulnerable to a clickjacking security attack. In clickjacking attacks, pages can be in an iframe on a malicious page, and users could be tricked into choosing buttons to take actions they're not aware of. When designing your page, you should be aware of this and make sure you're not exposing any functionality in the page for the part that would be dangerous if surfaced in a malicious page.</span></span>
 

 
<span data-ttu-id="177fe-p146">Obwohl Benutzer manuell eine andere Größe für Ihr Part einstellen können, können Sie in der Part-Definition eine bestimmte Größe für das Part festlegen. Außerdem können Sie über **postmessages** anfordern, dass die Größe Ihres Parts dynamisch angepasst wird. Als Standard wird empfohlen, für das Part eine Größe in Schritten von 30 px (z. B. 150 px oder 210 px zu wählen. Wenn dann Parts verschiedener Add-Ins gemischt auf einer Seite vorhanden sind, kann der Benutzer trotzdem den Eindruck vermittelt bekommen, dass jedes dieser Parts speziell für diesen Ort erstellt wurde. Wenn Ihr Part eine Kachel der Erste Schritte-Funktion imitieren soll, muss es eine Höhe und Breite von 150 px haben. Wenn das Part in einer Spalte angezeigt werden soll, um Details zu zeigen, sollte es eine Breite von 300 px haben.</span><span class="sxs-lookup"><span data-stu-id="177fe-p146">Although users can manually set a different size on your part, you are able to set a particular size for the part in the part definition. You also have the ability to request that your part is resized dynamically through  **postmessages**. By default, we recommend that your part choose sizes in increments of 30px (for example, 150px or 210px) so that when parts from different add-ins are mixed on the same page, the user can still get a sense that each of the parts was built to work in the same space. If your part is meant to mimic a tile from the getting started experience, it should have a height and width of 150px. If the part is meant to display in a side column to show details, it should have a width of 300px.</span></span>
 

 
<span data-ttu-id="177fe-p147">Wenn Ihr Part dynamischen Inhalt anzeigt, empfiehlt es sich, eine Größenanpassung anzufordern, um das Einbetten von Bildlaufleisten auf einer Seite zu reduzieren. Das folgende Beispiel zeigt, wie Sie **postmessages** verwenden, um die Größe des Parts anzupassen:</span><span class="sxs-lookup"><span data-stu-id="177fe-p147">If your part displays dynamic content, it's a good idea to request a resize to reduce having scrollbars embedded within a page. The following example shows you how to use  **postmessages** to resize the part:</span></span>
 

 



```
window.parent.postMessage('<message senderId={your ID}>resize(120, 300)</message>', {hostweburl});
```

<span data-ttu-id="177fe-p148">Im obigen Beispiel wird der **senderId**-Wert in der Abfragezeichenfolge der Seite automatisch durch den Add-In-Webpart-Code festgelegt, wenn die Seite gerendert wird. Ihre Seite liest dann einfach den **SenderId**-Wert aus der Abfragezeichenfolge und verwendet ihn beim Anfordern einer Größenanpassung. Sie können die Hostweb-URL aus der Abfragezeichenfolge abrufen, indem Sie in der Definition des Add-In-Webparts die Token **StandardTokens** oder **HostUrl** an das **Src** -Attribut anfügen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p148">In the example above, the  **senderId** value will be set on the query string of the page automatically by the add-in part code when the page is rendered. Your page would just need to read the **SenderId** value off of the query string and use it when requesting a resize. You can retrieve the host web URL from the query string by appending the **StandardTokens** or **HostUrl** tokens to the **Src** attribute in your add-in part definition.</span></span>
 

 
<span data-ttu-id="177fe-p149">Um ein Part für die Hostwebsite anzugeben, müssen Sie ein Client-Webpart in der Feature-Datei im Add-In-Paket angeben (nicht die Feature-Datei im WSP-Paket). Sie können ein Part erstellen, das vom Endbenutzer konfigurierbar ist, z. B. durch Angabe einer Postleitzahl. Das folgende Markup spezifiziert ein Add-In-Part, und das Element **Properties** ist optional:</span><span class="sxs-lookup"><span data-stu-id="177fe-p149">To specify a part for the host web, you must specify a client Web Part in the feature file in the add-in package (not the feature file in the WSP in the package). You can create a part that could be configurable by the end user, such as by specifying a ZIP or postal code. The following markup specifies an add-in part, and the  **Properties** element is optional:</span></span>
 

 



```XML
<ClientWebPart 
    Name="Sample Add-in Part" 
    DefaultWidth="600" 
    DefaultHeight="300" 
    Title="Sample Add-in Part" 
    Description="This is a sample part with properties.">
    <Content Type="html" Src="~appWebUrl/Pages/Part.aspx?Property1=_prop1_&amp;amp;Property2=_prop2_&amp;amp;Property3=_prop3_&amp;amp;Property4=_prop4_" />
    <Properties>
        <Property 
            Name="prop1" 
            Type="string" 
            WebBrowsable="true" 
            WebDisplayName="First Property" 
            WebDescription="Description 1" 
            WebCategory="Custom Properties" 
            DefaultValue="String Property" 
            RequiresDesignerPermission="true" />
        <Property 
            Name="prop2" 
            Type="boolean" 
            WebBrowsable="true" 
            WebDisplayName="Second Property" 
            WebDescription="Description 2" 
            WebCategory="Custom Properties" 
            DefaultValue="TRUE" 
            RequiresDesignerPermission="true" />
        <Property 
            Name="prop3" 
            Type="int" 
            WebBrowsable="true" 
            WebDisplayName="Third Property" 
            WebDescription="Description 3" 
            WebCategory="Custom Properties" 
            DefaultValue="1" 
            RequiresDesignerPermission="true" />
        <Property 
            Name="prop4" 
            Type="enum" 
            WebBrowsable="true" 
            WebDisplayName="Fourth Property" 
            WebDescription="Description 4" 
            WebCategory="Custom Properties" 
            DefaultValue="one" 
            RequiresDesignerPermission="true" >
            <EnumItems>
                <EnumItem Value="one" WebDisplayName="One" />
                <EnumItem Value="two" WebDisplayName="Two" />
                <EnumItem Value="three" WebDisplayName="Three" />
            </EnumItems>
        </Property>
    </Properties>
</ClientWebPart>
```

<span data-ttu-id="177fe-485">In Ihrem **ClientWebPart**-Element können Sie Folgendes angeben:</span><span class="sxs-lookup"><span data-stu-id="177fe-485">In your  **ClientWebPart** element, you'll want to specify the following things:</span></span>
 

 

 

-  <span data-ttu-id="177fe-486">**Name:** Ein interner Name, der zum Identifizieren des Add-Ins verwendet wird. Der Name muss eindeutig sein.</span><span class="sxs-lookup"><span data-stu-id="177fe-486">**Name:** An internal name that is used to identify the add-in; must be unique.</span></span>
    
 
-  <span data-ttu-id="177fe-p150">**DefaultWidth/DefaultHeight:** Die Standardgröße des Webparts. Bei Bedarf können Sie die Größe der Seite innerhalb des Parts anpassen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p150">**DefaultWidth/DefaultHeight:** The default size of the Web Part. If necessary, you can resize the page inside the part.</span></span>
    
 
-  <span data-ttu-id="177fe-489">**Title:** Der Name, der für Endbenutzer angezeigt wird, wenn diese Ihr Part mit dem Feature zum Hinzufügen von Webparts zu einer Seite hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="177fe-489">**Title:** The name that is displayed to end users when they add your part to a page through the Web Part adder.</span></span>
    
 
-  <span data-ttu-id="177fe-490">**Description:** Die Beschreibung, die für Endbenutzer angezeigt wird, wenn diese Ihr Part mit dem Feature zum Hinzufügen von Webparts zu einer Seite hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="177fe-490">**Description:** The description that is shown to end users when they add your part to a page through the Web Part adder.</span></span>
    
 
<span data-ttu-id="177fe-p151">Sie können Part-Eigenschaften vom Typ **string**, **enum**, **int** und **Boolean** angeben. Sie können die **toolpart**-Kategorie angeben, in der Ihre Eigenschaften angezeigt werden sollen, indem Sie das Attribut **WebCategory** verwenden. Die Attribute für das **Property**-Element, die Sie angeben müssen, lauten wie folgt:</span><span class="sxs-lookup"><span data-stu-id="177fe-p151">You can specify part properties of type  **string**,  **enum**,  **int**, and  **Boolean**. You can specify the  **toolpart** category that you want your properties to appear in by using the **WebCategory** attribute. The attributes on the **Property** element that you want to specify are as follows:</span></span>
 

 

 

-  <span data-ttu-id="177fe-494">**Name:** Der Name, der verwendet wird, um diese Eigenschaft an einen Token in der Abfragezeichenfolge anzupassen, der ersetzt werden soll.</span><span class="sxs-lookup"><span data-stu-id="177fe-494">**Name:** The name used to match this property with a token on the query string to replace.</span></span>
    
 
-  <span data-ttu-id="177fe-495">**WebDisplayName:** Der Name, der im Toolpart verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="177fe-495">**WebDisplayName:** The name used in the tool part.</span></span>
    
 
-  <span data-ttu-id="177fe-496">**WebCategory:** Das Toolpart in dem Toolbereich, dem diese Eigenschaft hinzugefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="177fe-496">**WebCategory:** The tool part in the toolpane to add this property to.</span></span>
    
 
-  <span data-ttu-id="177fe-p152">**Type:** Der Eingabedatentyp, der vom Benutzer erwartet wird. Der Typ kann **string**, **enum**, **int** oder **Boolean** sein.</span><span class="sxs-lookup"><span data-stu-id="177fe-p152">**Type:** The input data type that is expected from the user. Type can be **string**,  **enum**,  **int**, or  **Boolean**.</span></span>
    
 
-  <span data-ttu-id="177fe-499">**DefaultValue:** Der Standardwert für Ihre Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="177fe-499">**DefaultValue:** The default value for your property.</span></span>
    
 
<span data-ttu-id="177fe-p153">Wenn das Part der Seite hinzugefügt wird, werden alle Zeichenfolgen in der Abfragezeichenfolge, die mit dem Muster _propertyName_ übereinstimmen, automatisch durch den Wert der Eigenschaft mit diesem Namen in der Webpartinstanz ersetzt, oder dem Standardnamen, wenn der Benutzer ihn nicht festgelegt hat. Anschließend führen Sie Code innerhalb der Seite aus, um die Abfragezeichenfolge zu parsen und die Eigenschaften zu extrahieren, um sie beim Rendering und bei Interaktionen auf Ihrer Seite zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="177fe-p153">When the part is added to the page, any strings in the query string that match the pattern _propertyName_ are automatically replaced with the value of the property with that Name on the Web Part instance, or the default value if the user hasn't set it. You would then run code inside the page to parse through the query string and pull out the properties to use them in rendering and interaction on your page.</span></span>
 

 
<span data-ttu-id="177fe-p154">Sie können auch veranlassen, dass die Webpart-ID in der Abfragezeichenfolge gesendet wird, indem Sie mithilfe der Zeichenfolge _wpid_ darstellen, wo in der Abfragezeichenfolge sie ersetzt werden soll. Dies kann bei der Unterscheidung verschiedener Part-Instanzen hilfreich sein, wenn Sie Informationen über Benutzerauswahlen oder -interaktionen auf einer Pro-Instanz-Basis speichern möchten. Weitere Informationen finden Sie unter  [Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In](create-add-in-parts-to-install-with-your-sharepoint-add-in.md).</span><span class="sxs-lookup"><span data-stu-id="177fe-p154">You can also choose to have the Web Part ID sent on the query string by using the _wpid_ string to represent where you want it to be replaced on the query string. This can be helpful in differentiating different part instances if you want to be able to store information about user choices or interactions on a per-instance basis. For more information, see  [Create add-in parts to install with your SharePoint Add-in](create-add-in-parts-to-install-with-your-sharepoint-add-in.md).</span></span>
 

 

### <a name="adding-custom-actions-to-the-host-web"></a><span data-ttu-id="177fe-505">Hinzufügen von benutzerdefinierten Aktionen zur Hostwebsite</span><span class="sxs-lookup"><span data-stu-id="177fe-505">Adding custom actions to the host web</span></span>

<span data-ttu-id="177fe-p155">Wenn Sie über Funktionen verfügen, die sinnvoll im Kontext von Listenelementen oder Dokumenten oder auf bestimmten Menübandregisterkarten in der Hostwebsite angezeigt werden könnten, können Sie sie dem Kontextmenü oder dem Menüband mithilfe von benutzerdefinierten Aktionen hinzufügen. Um benutzerdefinierte Aktionen auf der Hostwebsite anzuzeigen, müssen Sie sie in der gleichen Art von loser Feature-Datei im Add-In-Paket definieren, wie die Datei, die **ClientWebPart**-Definitionen enthält.</span><span class="sxs-lookup"><span data-stu-id="177fe-p155">If you have functionality that would make sense to surface in the context of list items or documents, or on particular ribbon tabs in the host web, you can add those to the context menu or the ribbon by using custom actions. To surface custom actions in the host web, you'll need to define them in the same kind of loose feature file in the add-in package as the one that contains  **ClientWebPart** definitions.</span></span>
 

 

<span data-ttu-id="177fe-508">**Abbildung 4. Eine benutzerdefinierte Aktion im Kontextmenü**</span><span class="sxs-lookup"><span data-stu-id="177fe-508">**Figure 4. A custom action in the contextual menu**</span></span>

 

 
![Eine benutzerdefinierte Aktion im Kontextmenü](../images/AppUXGuidelines_ECBcustomaction.png)
 
<span data-ttu-id="177fe-510">Der Code für benutzerdefinierte Aktionen, die in der Hostwebsite angezeigt werden, ist gleich wie in früheren Versionen von SharePoint, jedoch mit folgenden Einschränkungen:</span><span class="sxs-lookup"><span data-stu-id="177fe-510">The code for custom actions that are surfaced in the host web is the same as in previous versions of SharePoint, with the following restrictions:</span></span>
 

 

 

- <span data-ttu-id="177fe-511">Das **Location**-Attribut muss entweder **CommandUI.Ribbon** oder **EditControlBlock** sein.</span><span class="sxs-lookup"><span data-stu-id="177fe-511">The  **Location** attribute must be either **CommandUI.Ribbon** or **EditControlBlock**.</span></span>
    
 
-  <span data-ttu-id="177fe-512">**CustomAction** darf kein JavaScript enthalten:</span><span class="sxs-lookup"><span data-stu-id="177fe-512">**CustomAction** cannot contain JavaScript:</span></span>
    
      - <span data-ttu-id="177fe-p156">Alle **UrlActions** oder **CommandActions** müssen eine URL sein, zu der navigiert werden kann. Die URL kann zusätzlich zu den App-spezifischen Token mit normalen Token für benutzerdefinierten Aktionen parametrisiert werden.</span><span class="sxs-lookup"><span data-stu-id="177fe-p156">Any  **UrlActions** or **CommandActions** must be a URL to navigate to. The URL can be parameterized with normal custom actions tokens in addition to the app-specific tokens.</span></span>
    
 
  -  <span data-ttu-id="177fe-515">**EnabledScript** ist bei Menübandanpassungen nicht zulässig.</span><span class="sxs-lookup"><span data-stu-id="177fe-515">**EnabledScript** is not allowed in ribbon customizations.</span></span>
    
 
<span data-ttu-id="177fe-p157">Normalerweise wird ein Benutzer bei Auswahl einer benutzerdefinierten Aktion zu der URL navigiert, die Sie mit den Token angegeben haben, die basierend auf der Benutzerauswahl aufgelöst wurden. In einigen Fällen soll der Benutzer jedoch auf der Seite bleiben, z. B. für schnelle Aktionen an einem bestimmten Dokument. Wenn Ihre benutzerdefinierte Aktion ein Dialogfeld öffnen soll anstatt Navigation zu ermöglichen, fügen Sie dem **CustomAction**-Element die folgenden Attribute hinzu.</span><span class="sxs-lookup"><span data-stu-id="177fe-p157">Normally when a user chooses a custom action, it will navigate them to the URL you have specified with any tokens resolved based on their selections. However, there are some cases where you might want the user to stay in context on the page, such as for quick actions on a particular document. If you want to have your custom action open a dialog box instead of navigating, you should add the following attributes to the  **CustomAction** element.</span></span>
 

 



```
HostWebDialog="TRUE"
HostWebDialogHeight="500" 
HostWebDialogWidth="500"
```

<span data-ttu-id="177fe-p158">Das Attribut **HostWebDialogHeight** und das Attribut **HostWebDialogWidth** sind optional. Wenn die Attribute nicht angegeben werden, wird die Standardgröße für ein Dialogfeld in SharePoint verwendet. Sie sollten jedoch generell die Größe Ihres Dialogfelds angeben, damit es passend aussieht und nicht mit Bildlaufleisten für den Benutzer angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="177fe-p158">The  **HostWebDialogHeight** attribute and the **HostWebDialogWidth** attribute are optional. If the attributes are not specified, the default size for a dialog box in SharePoint will be used. In general, though, you should specify the size of your dialog box so that it looks right and doesn't use scrollbars when it is displayed to the user.</span></span>
 

 
<span data-ttu-id="177fe-p159">Das Dialogfeld enthält immer eine Schaltfläche **Schließen** im Dialogfeld-Chrom. Sie können auf Ihrer Seite auch Schaltflächen hinzufügen, die das Dialogfeld schließen und der Ursprungsseite mitteilen, ob sie aktualisiert werden muss. Wenn Sie einen Schritt durchgeführt haben, der sich auf die Ansicht auswirken könnte, die der Benutzer anzeigt (z. B. das Aktualisieren von Eigenschaften in einem Dokument), sollten Sie die Seite aktualisieren. Wenn Sie dagegen keine Aktualisierung vorgenommen haben, sondern nur eine „Abbrechen“-Aktion durchgeführt oder eine Datei an ein Archiv gesendet haben, ohne Eigenschaften zu aktualisieren, können Sie der Seite mitteilen, dass keine Aktualisierung erforderlich ist. Die folgenden Beispiele zeigen, wie Sie POST-Meldungen senden können, um das Dialogfeld zu schließen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p159">The dialog box always includes a  **Close** button in the dialog box chrome. You can also include buttons on your page that will close the dialog box and tell the originating page whether it needs to refresh. If you've done something that could be reflected in the view the user is looking at (for example: updating properties on a document), you should refresh the page. On the other hand, if you didn't update anything (for example: a "cancel" action or sending a file to an archive without updating any properties), you can tell the page that no refresh is necessary. The following examples show you how to send POST messages to close the dialog box.</span></span>
 

 



```
window.parent.postMessage('CloseCustomActionDialogRefresh', '*');
window.parent.postMessage('CloseCustomActionDialogNoRefresh', '*');
```

<span data-ttu-id="177fe-527">Je nachdem, ob Sie **CloseCustomActionDialogRefresh** oder **CloseCustomActionDialogNoRefresh** verwenden, wird das Dialogfeld geschlossen und aktualisiert die zugehörige Seite oder nicht.</span><span class="sxs-lookup"><span data-stu-id="177fe-527">Depending on whether you use  **CloseCustomActionDialogRefresh** or **CloseCustomActionDialogNoRefresh**, the dialog box closes, and it either refreshes the page behind it or it does not.</span></span>
 

 
<span data-ttu-id="177fe-p160">Sie können dem Menüband der Hostwebsite von Ihrem Add-In aus keine benutzerdefinierte Registerkarte hinzufügen. Sie können nur benutzerdefinierte Gruppen oder einzelne Steuerelemente hinzufügen. Überschreiben Sie keines der standardmäßigen Steuerelemente im SharePoint-Menüband. Ihre Steuerelemente und die SharePoint-Steuerelemente sollten sich nebeneinander befinden.</span><span class="sxs-lookup"><span data-stu-id="177fe-p160">You cannot add a custom tab to the ribbon of the host web from your add-in. You can only add custom groups or individual controls. You should not override any of the default SharePoint ribbon controls. You should have your controls exist side-by-side with the SharePoint controls.</span></span>
 

 
<span data-ttu-id="177fe-p161">Wenn einige Ihrer Steuerelemente in einem Zusammenhang miteinander stehen oder der Benutzer sie in Zusammenhang mit der Verwendung Ihres Add-Ins empfindet, sollten Sie diese in einer eigenen benutzerdefinierten Gruppe zusammenfassen, damit der Benutzer sie leichter finden kann. Wenn dagegen die von Ihnen hinzugefügten Funktionen mit großer Wahrscheinlichkeit vom Benutzer als Teil der Gesamtwirkung seiner Website betrachtet, sollten Sie versuchen, das betreffende Steuerelement an einer logischen Position in den bestehenden Menübandpositionen einzufügen. Weitere Informationen finden Sie unter  [Gewusst wie: Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit Add-Ins für SharePoint](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="177fe-p161">If you have a few controls that are related to each other, or that the user will likely associate with using your add-in, you should group them in their own custom group so that the user is more likely to find them. If, on the other hand, the functionality you're adding is more likely to be something the user considers part of the core experience of their site, you should try to fit that control into a logical spot in the existing ribbon locations. For more information, see  [Create custom actions to deploy with SharePoint Add-ins](create-custom-actions-to-deploy-with-sharepoint-add-ins.md).</span></span>
 

 

## <a name="providing-a-settings-page-for-add-in-configuration"></a><span data-ttu-id="177fe-535">Bereitstellen einer Einstellungsseite für die Add-In-Konfiguration</span><span class="sxs-lookup"><span data-stu-id="177fe-535">Providing a settings page for add-in configuration</span></span>
<span data-ttu-id="177fe-536"><a name="UXGuide_Settings"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-536"><a name="UXGuide_Settings"> </a></span></span>

<span data-ttu-id="177fe-p162">In vielen Fällen ist sinnvoll, Ihr Add-In über Konfigurationsinformationen verfügen zu lassen, die der Benutzer ändern kann, und diese Informationen über eine Einstellungsseite bereitzustellen. Idealerweise wählen Sie vernünftige Standardwerte für diese Einstellungen, und Benutzer können dann zur Einstellungsbenutzeroberfläche wechseln, wenn sie diese Standardwerte ändern müssen. In einigen Fällen erfordert das Add-In die Angabe bestimmter Informationen oder die Auswahl von Optionen, ehe es funktioniert. Wenn für Ihr Add-In Informationen erforderlich sind, bevor es funktionieren kann, sollten Sie eine benutzerfreundliche Möglichkeit vorsehen, mit der der Benutzer zur Einstellungsseite geleitet wird, um die Konfiguration zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="177fe-p162">In many cases, it makes sense for your add-in to have some configuration information that the user can change, and to expose this information through the use of a settings page. Ideally, you can choose reasonable defaults for those settings, and users can choose to go to the settings UI only if they need to modify those defaults. In some cases, the add-in will require certain information or choices to be provided before the add-in can function. When your add-in requires information before it can function, you should provide a user experience that guides the user to the settings page to update the configuration.</span></span>
 

 
<span data-ttu-id="177fe-p163">Fügen Sie ggf. die URL der Einstellungsseite im rechten oberen Menü dem Add-In hinzu, damit Benutzer sie problemlos finden können. Wenn Ihr Add-In über eine Erste Schritte-Funktion oder andere Einstellungen verfügt, können Sie diese ebenfalls hinzufügen. Weitere Informationen finden Sie unter  [Verwenden des Client-Chromsteuerelements in Add-Ins für SharePoint](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span><span class="sxs-lookup"><span data-stu-id="177fe-p163">You should add the settings page URL to the app's top-right menu if appropriate so that users can find it easily. If your add-in has a getting started experience or other settings, you can add those also. For more information, see  [Use the client chrome control in SharePoint Add-ins](use-the-client-chrome-control-in-sharepoint-add-ins.md).</span></span>
 

 
<span data-ttu-id="177fe-p164">Sie sollten auch berücksichtigen, dass der Benutzer, der Ihr Add-In besucht, möglicherweise nicht in der Lage ist, es zu konfigurieren. Auch Ihre Benutzeroberfläche sollte nicht voraussetzen, dass der aktuelle Benutzer die Konfiguration durchführen kann. Ihr Add-In sollte den Benutzer führen und ihm ermöglichen, die richtige Person zu finden, wenn er die Konfiguration nicht selbst vornehmen kann.</span><span class="sxs-lookup"><span data-stu-id="177fe-p164">You should also keep in mind that the user who is currently visiting the add-in might not be able to configure it. Your UI should also not assume that the current user is able to complete the configuration. Your add-in should guide the user to find the right person if they cannot configure it.</span></span>
 

 

## <a name="managing-user-licenses-in-add-ins"></a><span data-ttu-id="177fe-547">Verwalten von Benutzerlizenzen in Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-547">Managing user licenses in add-ins</span></span>
<span data-ttu-id="177fe-548"><a name="UXGuide_License"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-548"><a name="UXGuide_License"> </a></span></span>

<span data-ttu-id="177fe-549">Wenn Ihr Add-In nicht kostenlos ist, sollten Sie ein gutes Gleichgewicht finden zwischen den Features, die im Testmodus bzw. im unlizenzierten Modus verfügbar oder eingeschränkt sind, und der kostenpflichtigen Version.</span><span class="sxs-lookup"><span data-stu-id="177fe-549">If your add-in is not free, you should find a good balance between the features that are available or restricted in the trial or unlicensed modes versus the fully paid version.</span></span>
 

 
<span data-ttu-id="177fe-p165">Wenn Sie eine zeitlich begrenzte Testversion bereitstellen, sollte sie im Testzeitraum gleich wie die kostenpflichtige Version funktionieren. Ermöglichen Sie Benutzern einen realistischen Eindruck davon, was sie bekommen, wenn sie für das Add-In bezahlen. Wenn Sie im Testzeitraum Einschränkungen vorsehen, geben Sie klare Informationen, wie der Benutzer diese aufheben kann, wenn er bezahlt. Bei zeitlich unbegrenzten Testversionen sollten Sie so viele Funktionen freigeben, wie Ihrer Meinung nach erforderlich sind, damit der Benutzer den Wert Ihres Add-Ins gut einschätzen kann. Stellen Sie klar heraus, welche zusätzlichen Vorteile es bringen würde, für das Add-In zu bezahlen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p165">If you provide a time-limited trial, the trial version should act just like the paid version during the trial period. Give users a realistic expectation of what they will get when they pay for the add-in. If you choose to restrict anything during the trial period, be very clear about how the user can get more when they pay. For unlimited trials, you should expose as much functionality as you think is needed for the user to get a good sense of the value of your add-in. Make it clear what extra benefits they would get by paying for it.</span></span>
 

 
<span data-ttu-id="177fe-p166">Wenn Benutzer Ihr Add-In zum ersten Mal sehen, besitzen sie möglicherweise keine Lizenz dafür. Zum Beispiel könnte ein Benutzer Ihr Add-In einer Team-Website hinzufügen, jedoch vergessen, die anderen Benutzer zu lizenzieren. Andere Benutzer der Team-Website würden dann Ihr Add-In ohne Lizenz nutzen, bis der Lizenzmanager die Situation behebt. Stellen Sie sicher, dass Benutzer einen guten Eindruck erhalten, denn dann steigt die Wahrscheinlichkeit, dass eine Lizenz verlangt oder gekauft wird. Es empfiehlt sich, Benutzern grundsätzlich die Anzeige und Navigation der Daten in Ihrem Add-In zu ermöglichen. Stellen Sie heraus, dass eine Lizenz mehr Features bedeutet, weisen Sie jedoch nicht mehr als einmal pro Sitzung darauf hin.</span><span class="sxs-lookup"><span data-stu-id="177fe-p166">When people first see your add-in, they may not have a license for it. For example, one user might add your add-in to a team site, but forget to license anyone else. Other users on the team site would be using your add-in without a license until the license manager fixes the situation. You should make sure they get a good impression so they will be more likely to demand or buy a license. It is a good idea to always let users view and navigate through the data in your add-in. Be clear about how having a license will enable more features, but don't remind them more than once per session.</span></span>
 

 
<span data-ttu-id="177fe-p167">Wenn der Hauptnutzen Ihres Add-Ins im Anzeigen von Daten besteht (und sie diese nicht kostenlos weitergeben möchten), sollten Sie ein begrenztes Subset der Daten verfügbar machen oder die Daten ohne Interaktivität anzeigen. Hindern Sie Benutzer ohne Lizenz nicht daran, Ihr Add-In anzuzeigen. Unlizensierte Benutzer sollten einen Eindruck davon erhalten, welchen Nutzen Ihr Add-In ihnen bringen kann. Dadurch wird die Wahrscheinlichkeit größer, dass sie es kaufen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p167">If your app's core value is in displaying data (and you don't want to give that away for free), you should show a limited subset of the data, or show the data without any interactivity. You should not block unlicensed users from viewing your add-in. Unlicensed users should get a taste of what your add-in can do for them so that they are more likely to buy it.</span></span>
 

 

### <a name="encouraging-users-to-get-a-license"></a><span data-ttu-id="177fe-564">Förderung des Erwerbs von Lizenzen</span><span class="sxs-lookup"><span data-stu-id="177fe-564">Encouraging users to get a license</span></span>

<span data-ttu-id="177fe-p168">Wenn unlizenzierte Benutzer bzw. Benutzer der Testversion Ihr Add-In verwenden, sollten Sie sie zum Erwerb einer Volllizenz ermutigen:</span><span class="sxs-lookup"><span data-stu-id="177fe-p168">In the case where an unlicensed or trial license user is using your add-in, you should encourage them to get a full license. There are two ways to encourage users to get a full license:</span></span>
 

 

- <span data-ttu-id="177fe-567">Durch eine Statusleiste oben auf der Seite, die den Lizenzstatus angibt.</span><span class="sxs-lookup"><span data-stu-id="177fe-567">With a status bar at the top of the page that indicates their license state.</span></span>
    
 
- <span data-ttu-id="177fe-568">Im Kontext, wenn ein Benutzer versucht, auf Inhalte oder Funktionen zuzugreifen, für die eine Lizenz erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="177fe-568">In context when the user tries to access content or functionality that requires a license.</span></span>
    
 
<span data-ttu-id="177fe-p169">Achten Sie sorgfältig darauf, zweite Lizenzwarnungen nicht übermäßig einzusetzen. Es ist für den Benutzer eine bessere Erfahrung, wenn Sie die Statusmeldung der obersten Ebene verwenden und alle unlizenzierten Funktionen deaktivieren, und den Benutzer nicht unangenehm überraschen, weil er einen Schritt nicht durchführen kann. In beiden Fällen sollte Ihre Meldung verbindlich und ermutigend sein und nicht unfreundlich. Sehen Sie einen Link zur Storefront-Add-In-Detailseite vor, auf der der Benutzer eine Lizenz erwerben kann.</span><span class="sxs-lookup"><span data-stu-id="177fe-p169">You should be very careful about overusing the second case of license warnings. It is a better experience for the user when you use the top-level status message and disable any unlicensed functionality than to let the user be unpleasantly surprised by an inability to do something. In either case, your message should be friendly and encouraging rather than stern. You should give the user a link to the storefront add-in details page for your add-in, where they can get a license.</span></span>
 

 

### <a name="licensing-status-bar"></a><span data-ttu-id="177fe-573">Statusleiste für die Lizenzierung</span><span class="sxs-lookup"><span data-stu-id="177fe-573">Licensing status bar</span></span>

<span data-ttu-id="177fe-p170">SharePoint verfügt über eine integrierte Statusleiste, die Sie auf SharePoint-Seiten verwenden können, indem Sie die JavaScript-API aufrufen. Sie können auch das Format der integrierten Statusleiste kopieren. Verwenden Sie gelbe "Warnfarbe" zusammen mit einer für die Benutzersituation geeigneten, wie beispielsweise:</span><span class="sxs-lookup"><span data-stu-id="177fe-p170">SharePoint has a built-in status bar that you can use on SharePoint pages by calling the JavaScript API. You can also copy the styling of the built-in status bar. You should use the yellow "warning"" color, with a message appropriate to the situation the user is in, for example:</span></span>
 

 

- <span data-ttu-id="177fe-p171">Für Benutzer einer **zeitlich unbegrenzten** Testversion: Dies ist eine Testversion von _<app name>_. Hier können Sie die Vollversion erwerben und _<paid functionality>_ freischalten.</span><span class="sxs-lookup"><span data-stu-id="177fe-p171">For users of an  **unlimited trial**: This is a trial version of _<app name>_. Go here to purchase the full version and unlock  _<paid functionality>_.</span></span>
    
 
- <span data-ttu-id="177fe-p172">Für Benutzer einer **noch nicht abgelaufenen, zeitlich begrenzten Testversion**: In _<Zeitraum, ausgedrückt durch eine leicht verständliche Zahlenangabe wie „3 Tage“, nicht „73:42:12“>_ läuft diese Testversion von _<app name>_ ab. Hier können Sie die Vollversion erwerben, um den ganzen Funktionsumfang nutzen zu können.</span><span class="sxs-lookup"><span data-stu-id="177fe-p172">For users of an  **unexpired time-limited trial**: There [is|are] _<amount of time, expressed in a human-readable metric like "3 days" not "73:42:12">_ left in this trial of _<app name>_. Go here to purchase the full version and ensure you don't miss a moment of full functionality.</span></span>
    
 
- <span data-ttu-id="177fe-p173">Für Benutzer einer **zeitliche begrenzten Testversion, die abgelaufen ist**: Leider ist der Testzeitraum für diese Testversion von _<app name>_ abgelaufen. Hier können Sie die Vollversion erwerben und den gesamten Funktionsumfang nutzen.</span><span class="sxs-lookup"><span data-stu-id="177fe-p173">For users of an  **expired time-limited trial**: Unfortunately, there is no more time left in this trial of _<app name>_. Go here to purchase the full version and return to full functionality.</span></span>
    
 
- <span data-ttu-id="177fe-p174">Für Benutzer **ohne Lizenz**: Leider besitzen Sie keine Lizenz für _<app name>_. Hier können Sie die Vollversion erwerben und _<paid functionality>_ aktivieren.</span><span class="sxs-lookup"><span data-stu-id="177fe-p174">For users  **without any license**: Unfortunately, you don't have a license for _<app name>_. Go here to purchase the full version and enable  _<paid functionality>_.</span></span>
    
 

## <a name="other-design-considerations-for-sharepoint-add-ins"></a><span data-ttu-id="177fe-585">Sonstige Überlegungen zum Design von SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-585">Other design considerations for SharePoint Add-ins</span></span>
<span data-ttu-id="177fe-586"><a name="UXGuide_Other"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-586"><a name="UXGuide_Other"> </a></span></span>

<span data-ttu-id="177fe-587">Zusätzlich zu den bereits behandelten Informationen sollten Sie noch folgende Punkte berücksichtigen, wenn Sie Ihr Add-In für SharePoint erstellen.</span><span class="sxs-lookup"><span data-stu-id="177fe-587">In addition to what has already been explored, you should keep these things in mind when you are creating your SharePoint Add-in.</span></span>
 

 

### <a name="persisting-necessary-information-in-cookies"></a><span data-ttu-id="177fe-588">Speichern von notwendigen Informationen in Cookies</span><span class="sxs-lookup"><span data-stu-id="177fe-588">Persisting necessary information in cookies</span></span>

<span data-ttu-id="177fe-p175">Ihr Add-In benötigt sehr viele Informationen für die Interaktion mit SharePoint, z. B. die URL der Hostwebsite oder die POST-Meldung mit SharePoint-Anmeldeinformationen. Wenn Informationen in einem Client-Cookie gespeichert werden, muss Ihr Add-In nicht immer wieder diese Informationen erneut von SharePoint anfordern, sodass sich für den Endbenutzer eine angenehmere effizientere Nutzungserfahrung ergibt.</span><span class="sxs-lookup"><span data-stu-id="177fe-p175">There will be a lot of information that your add-in will need to be able to interact with SharePoint, such as the URL of the host site or the POST message with SharePoint credentials. Persisting information in a client cookie means that your add-in doesn't have to keep requesting the information from SharePoint, which leads to a smoother, better-performing experience for the end user.</span></span>
 

 

### <a name="requesting-a-new-oauth-token"></a><span data-ttu-id="177fe-591">Anfordern eines neuen OAuth-Tokens</span><span class="sxs-lookup"><span data-stu-id="177fe-591">Requesting a new OAuth token</span></span>

<span data-ttu-id="177fe-p176">Wenn Ihr Add-In über keine Anmeldeinformationen verfügt, können Sie ein neues Token anfordern. Leiten Sie dazu den Benutzer mit Ihrer Add-In-ID und der URL, die er aufrufen möchte, zur Umleitungsseite. Die URL muss sich unter der Domäne der Umleitungs-URL befinden, die für die von Ihnen verwendete OAuth-App-ID registriert ist. Die folgende URL bietet ein Beispiel für die Vorgehensweise zum Umleiten Ihrer Add-In-Benutzer. (Platzhalter stehen in Klammern.)</span><span class="sxs-lookup"><span data-stu-id="177fe-p176">If your add-in doesn't have credentials, you can request a new one by redirecting the user to the redirect page with your add-in ID and the URL that the user is trying to go to. The URL must be under the domain of the redirect URL that is registered for the OAuth add-in ID that you are using. The following URL is an example of how to redirect your add-in users. (Placeholders are in braces.)</span></span>
 

 
 `{hostWebURL}/_layouts/15/appredirect.aspx?client_id={OAuth_app_ID}&amp;redirect_uri={redirectUrl}`
 

 

### <a name="checking-for-read-only-mode-on-sharepoint-sites"></a><span data-ttu-id="177fe-596">Überprüfen des schreibgeschützten Modus auf SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="177fe-596">Checking for read-only mode on SharePoint sites</span></span>

<span data-ttu-id="177fe-p177">Aufgrund von Aktualisierungen oder Wartungsarbeiten an der Website kann sich SharePoint manchmal im schreibgeschützten Modus befinden, wenn der Benutzer auf Ihr Add-In zugreift. Wenn Sie die Bearbeitung von SharePoint-Daten durch den Benutzer zulassen möchten, müssen Sie sicherstellen, dass Sie dem Benutzer keine Änderungen erlauben, die nicht auf den Server zurückgespeichert werden können. Deaktivieren Sie die Bearbeitungsbenutzeroberfläche im schreibgeschützten Modus. Um zu überprüfen, ob sich die Website im schreibgeschützten Modus befindet, können Sie diese API aufrufen:</span><span class="sxs-lookup"><span data-stu-id="177fe-p177">Due to upgrades or site maintenance, there might be times when SharePoint is in read-only mode at the moment the user accesses your add-in. If you're going to allow the user to manipulate SharePoint data, you should make sure you don't let the user make changes that can't be saved back to the server. Disable the editing UI when in read-only mode. To check if the site is in read-only mode, you can call this API:</span></span>
 

 
 `{hostWebUrl}/_api/site/ReadOnly`
 

 

## <a name="additional-resources"></a><span data-ttu-id="177fe-601">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="177fe-601">Additional resources</span></span>
<span data-ttu-id="177fe-602"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="177fe-602"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="177fe-603">UX-Design für SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-603">UX design for SharePoint Add-ins</span></span>](ux-design-for-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="177fe-604">Erstellen von UX-Komponenten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="177fe-604">Create UX components in SharePoint</span></span>](create-ux-components-in-sharepoint.md)
    
 
-  [<span data-ttu-id="177fe-605">Verwenden des Stylesheets einer SharePoint-Website in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-605">Use a SharePoint website's style sheet in SharePoint Add-ins</span></span>](use-a-sharepoint-website-s-style-sheet-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="177fe-606">Verwenden des Client-Chromsteuerelements in SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-606">Use the client chrome control in SharePoint Add-ins</span></span>](use-the-client-chrome-control-in-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="177fe-607">Erstellen von Add-In-Webparts zur Installation mit Ihrem SharePoint-Add-In</span><span class="sxs-lookup"><span data-stu-id="177fe-607">Create add-in parts to install with your SharePoint Add-in</span></span>](create-add-in-parts-to-install-with-your-sharepoint-add-in.md)
    
 
-  [<span data-ttu-id="177fe-608">Erstellen benutzerdefinierter Aktionen zur Bereitstellung mit SharePoint-Add-Ins</span><span class="sxs-lookup"><span data-stu-id="177fe-608">Create custom actions to deploy with SharePoint Add-ins</span></span>](create-custom-actions-to-deploy-with-sharepoint-add-ins.md)
    
 
-  [<span data-ttu-id="177fe-609">Anpassen einer Listenansicht in SharePoint-Add-Ins durch clientseitiges Rendering</span><span class="sxs-lookup"><span data-stu-id="177fe-609">Customize a list view in SharePoint Add-ins using client-side rendering</span></span>](customize-a-list-view-in-sharepoint-add-ins-using-client-side-rendering.md)
    
 

 

 

