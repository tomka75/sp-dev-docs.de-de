---
title: Branding von Codeausschnitten mithilfe von CSS in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: d18d07b6-1a6b-4589-a65c-932b67cef595
ms.openlocfilehash: 4ed891c06956c4d2ff79cd681b81a3869a03cc3c
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="brand-snippets-by-using-css-in-sharepoint"></a><span data-ttu-id="700a4-102">Branding von Codeausschnitten mithilfe von CSS in SharePoint</span><span class="sxs-lookup"><span data-stu-id="700a4-102">How to: Brand snippets by using CSS in SharePoint</span></span>

<span data-ttu-id="700a4-103">Um einen Codeausschnitt zu formatieren, überschreiben Sie die Standardformatvorlagen mit benutzerdefiniertem CSS.</span><span class="sxs-lookup"><span data-stu-id="700a4-103">To style a snippet, you override the default styles with custom CSS.</span></span> <span data-ttu-id="700a4-104">Sie können CSS-IDs und Elementselektoren verwenden, um alle auf Elemente angewendeten Standardformatvorlagen zu überschreiben, oder Sie können einen HTML-Editor oder ein Tool wie die F12-Entwicklertools in Internet Explorer verwenden, um bestimmte Standardformatvorlagen zu identifizieren und zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="700a4-104">You can use CSS IDs and element selectors to override all the default styles applied to elements, or you can use an HTML editor or a tool such as the F12 developer tools in Internet Explorer to identify and override specific default styles.</span></span>

## <a name="introduction-to-styling-snippets-with-css"></a><span data-ttu-id="700a4-105">Einführung in die Formatierung von Codeausschnitten mit CSS</span><span class="sxs-lookup"><span data-stu-id="700a4-105">Introduction to styling snippets with CSS</span></span>
<span data-ttu-id="700a4-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="700a4-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="700a4-107">Nachdem Sie eine HTML-Masterseite konvertiert oder ein HTML-Seitenlayout erstellt haben, können Sie diese Seite in der serverseitigen Vorschau des Entwurfs-Managers anzeigen.</span><span class="sxs-lookup"><span data-stu-id="700a4-107">After you convert an HTML master page or create an HTML page layout, you can preview that page in the Design Manager server-side preview.</span></span> <span data-ttu-id="700a4-108">Von der Vorschauseite aus können Sie zum Codeausschnittkatalog navigieren und dann Codeausschnitte in die HTML-Datei kopieren.</span><span class="sxs-lookup"><span data-stu-id="700a4-108">From the preview page, you can navigate to the Snippet Gallery and then copy snippets to your HTML file.</span></span> <span data-ttu-id="700a4-109">Ein Ausschnitt ist eine HTML-Darstellung eines SharePoint-Steuerelements, z. B. ein Steuerelement der oberen Navigationsleiste oder ein Suchfeld.</span><span class="sxs-lookup"><span data-stu-id="700a4-109">A snippet is an HTML representation of a SharePoint control such as a top navigation control or a search box.</span></span>
  
    
    
<span data-ttu-id="700a4-110">Nachdem Sie einen Codeausschnitt in die HTML-Datei auf dem zugeordneten Laufwerk kopiert und dann die Änderungen gespeichert haben, können Sie die serverseitige Vorschau der HTML-Datei aktualisieren, um zu sehen, wie das Steuerelement gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="700a4-110">After you copy a snippet into the HTML file in your mapped drive and then save the changes, you can refresh the server-side preview of the HTML file to see how the control is rendered.</span></span> <span data-ttu-id="700a4-111">Codeausschnitte enthalten Markup, das eine Entwurfszeitvorschau in Ihrem gewünschten HTML-Editor bereitstellt, Sie sollten dieses Markup jedoch nicht bearbeiten, da es schreibgeschützt ist und Auswirkungen darauf hat, wie das Steuerelement auf dem Server gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="700a4-111">Snippets contain markup that provides a design-time preview in your HTML editor of choice, but you shouldn't edit this markup because it's read-only and doesn't affect how the control is rendered on the server.</span></span> <span data-ttu-id="700a4-112">Die serverseitige Vorschau hingegen ist eine Vorschau in voller Genauigkeit mit Live-Daten, falls verfügbar, ein Navigationssteuerelement zeigt z. B. die aktuelle Navigationsstruktur der Website mit Live-Daten aus Ihrer Datenquelle, z. B.ein SharePoint-Terminologiespeicher für die verwaltete Navigation.</span><span class="sxs-lookup"><span data-stu-id="700a4-112">By contrast, the server-side preview shows a full-fidelity preview with live data, if available—for example, a navigation control will show the site's current navigation structure with live data from your data source, such as a SharePoint term store for managed navigation.</span></span>
  
> [!NOTE]
> <span data-ttu-id="700a4-113">Weitere Informationen zum Zuordnen eines Netzlaufwerks finden Sie unter [Vorgehensweise: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="700a4-113">[Note:](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md) For more information about mapping a network drive, see  How to: Map a network drive to the SharePoint Master Page Gallery.</span></span> 
  
    
    

<span data-ttu-id="700a4-114">Codeausschnitte erben ihre Formatvorlagen standardmäßig von SharePoint-Formatvorlagen, z. B. „corev15.css“.</span><span class="sxs-lookup"><span data-stu-id="700a4-114">By default, snippets inherit their styles from SharePoint style sheets such as corev15.css.</span></span> <span data-ttu-id="700a4-115">Um einen Codeausschnitt zu formatieren, müssen Sie diese Formatvorlagen mit Ihrem benutzerdefiniertem CSS überschreiben.</span><span class="sxs-lookup"><span data-stu-id="700a4-115">To style a snippet, you have to override these default styles with your custom CSS.</span></span> <span data-ttu-id="700a4-116">Zu diesem Zweck können Sie folgende Aktionen ausführen:</span><span class="sxs-lookup"><span data-stu-id="700a4-116">To do this, you can:</span></span>
  
    
    

- <span data-ttu-id="700a4-117">Verwenden Sie CSS-IDs und Elementselektoren, um die auf die ausgewählten Elemente angewendeten Formatvorlagen vollständig zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="700a4-117">Use CSS IDs and element selectors to completely override the default styles applied to the chosen elements.</span></span>
    
  
- <span data-ttu-id="700a4-118">Verwenden Sie browserbasierte Tools wie die F12-Entwicklertools in Internet Explorer, um die standardmäßigen Formatvorlagen in der serverseitigen Vorschau im Entwurfs-Manager zu prüfen, und identifizieren Sie dann bestimmte Formatvorlagen, die überschrieben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="700a4-118">Use a browser-based tool such as the F12 developer tools in Internet Explorer to inspect the default styles in the server-side preview in Design Manager, and then identify specific styles to override.</span></span>
    
  
- <span data-ttu-id="700a4-119">Verwenden Sie die Funktionen Ihres HTML-Editors, um die Standardformatvorlagen in der schreibgeschützten Vorschau eines Codeausschnitts zu prüfen, und identifizieren Sie dann bestimmte Formatvorlagen zum Überschreiben.</span><span class="sxs-lookup"><span data-stu-id="700a4-119">Use the features of your HTML editor to inspect the default styles in the read-only preview of a snippet, and then identify specific styles to override.</span></span> 
    
  
<span data-ttu-id="700a4-120">Um die Standardformatvorlagen mithilfe der Entwicklertools in Internet Explorer zu identifizieren, sollten Sie die serverseitige Vorschau im Entwurfs-Manager verwenden, um Ihre HTML-Masterseite oder das Seitenlayout anzuzeigen. Drücken Sie **F12**, um die Entwicklertools zu starten, wählen Sie das Menü **Suchen** aus, und wählen Sie dann **Element durch Klicken auswählen** aus.</span><span class="sxs-lookup"><span data-stu-id="700a4-120">To identify the default styles by using the developer tools in Internet Explorer, you should use the server-side preview in Design Manager to view your HTML master page or page layout, press **F12** to start the developer tools, choose the **Find** menu, and then choose **Select element by click**.</span></span> <span data-ttu-id="700a4-121">Dadurch können Sie auf Element auf der Seite klicken und genau sehen, welche Formatvorlagen überschrieben werden sollen, indem Sie CSS zu der benutzerdefinierten Formatvorlage hinzufügen, mit der Ihre HTML-Masterseite oder das Seitenlayout verknüpft ist.</span><span class="sxs-lookup"><span data-stu-id="700a4-121">This enables you to click elements on the page and see exactly what styles to override by adding CSS to the custom style sheet that your HTML master page or page layout links to.</span></span>
  
    
    
<span data-ttu-id="700a4-122">Die standardmäßigen SharePoint-Formatvorlagen enthalten viele Formatvorlagen, aufgrund derer es schwierig ist, bestimmte Formate zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="700a4-122">The default SharePoint style sheets contain many styles, which can make it challenging to identify specific styles.</span></span> <span data-ttu-id="700a4-123">Als Alternative zu browserbasierten Tools und in Abhängigkeit von Ihrem HTML-Editor ist es vielleicht einfacher, den Codeausschnitt aus dem Codeausschnittkatalog in Ihre HTML-Datei zu kopieren und dann den HTML-Editor zum Identifizieren von Formatvorlagen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="700a4-123">As an alternative to browser-based tools, and depending on your HTML editor, you may find it easier to copy the snippet from the Snippet Gallery into your HTML file, and then use the HTML editor to identify the styles.</span></span> <span data-ttu-id="700a4-124">Wenn Sie im Codeausschnittkatalog **Aktualisieren** und dann **In Zwischenablage kopieren** auswählen, enthält der Codeausschnitt eine HTML-Vorschau dieses Codeausschnitts.</span><span class="sxs-lookup"><span data-stu-id="700a4-124">In the Snippet Gallery, when you choose **Update** and then choose **Copy to Clipboard**, the snippet contains an HTML preview of that snippet.</span></span> <span data-ttu-id="700a4-125">Nachdem Sie den Codeausschnitt in Ihre HTML-Datei kopiert haben, können Sie die in der schreibgeschützten Vorschau verwendeten Formatvorlagen überprüfen, die im Codeausschnitt enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="700a4-125">After you copy the snippet into your HTML file, you can inspect the styles used in the read-only preview contained in the snippet.</span></span> <span data-ttu-id="700a4-126">Auf diese Weise analysieren Sie eine kleinere Teilmenge der Standardformatvorlagen.</span><span class="sxs-lookup"><span data-stu-id="700a4-126">This way, you are parsing a smaller subset of the default styles.</span></span>
  
    
    
<span data-ttu-id="700a4-127">In Abhängigkeit von dem Codeausschnitt und dem Umfang Ihrer Anpassung, möchten Sie vielleicht CSS-IDs und Elementselektoren verwenden, um alle Standardformatvorlagen vollständig zu überschreiben anstatt bestimmte Formatvorlagen für das Überschreiben auszuwählen.</span><span class="sxs-lookup"><span data-stu-id="700a4-127">Depending on the snippet and the extent of your customization, you may want to use CSS IDs and element selectors to completely override all of the default styles, instead of choosing specific default styles to override.</span></span> <span data-ttu-id="700a4-128">Im folgenden Beispiel wird veranschaulicht, wie diese Methode verwendet wird, um benutzerdefinierte Formatvorlagen auf den Codeausschnitt für die obere Navigationsleiste anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="700a4-128">The following example demonstrates how to use this method to apply custom styles to the top navigation snippet.</span></span>
  
    
    

## <a name="example-style-the-top-navigation-snippet"></a><span data-ttu-id="700a4-129">Beispiel: Codeausschnitt zum Formatieren der oberen Navigationsleiste</span><span class="sxs-lookup"><span data-stu-id="700a4-129">Example: Style the top navigation snippet</span></span>
<span data-ttu-id="700a4-130"><a name="Example"> </a></span><span class="sxs-lookup"><span data-stu-id="700a4-130"><a name="Example"> </a></span></span>

<span data-ttu-id="700a4-131">Der Codeausschnitt für die obere Nagivationsleiste ist einer der am häufigsten verwendeten Codeausschnitte, er ist daher auch einer der häufigsten Branding-Codeausschnitte.</span><span class="sxs-lookup"><span data-stu-id="700a4-131">The top navigation snippet is one of the most commonly used snippets, so it's also one of the most commonly branded snippets.</span></span> <span data-ttu-id="700a4-132">Auf einer SharePoint-Website können Sie eine Option zum Verwenden der verwalteten Navigation auswählen, sodass ein Terminologiespeicher die Datenquelle für den Codeausschnitt der oberen Navigationsleiste wird.</span><span class="sxs-lookup"><span data-stu-id="700a4-132">In a SharePoint site, you can select an option to use managed navigation, so that a term store becomes the data source for the top navigation snippet.</span></span> <span data-ttu-id="700a4-133">Auf diese Weise können Sie das Terminologiespeicher-Verwaltungstool unter **Websiteeinstellungen** verwenden, um Navigationsausdrücke hinzuzufügen oder zu löschen und die Navigationstaxonomie zu verwalten, die vom Codeausschnitt für die obere Navigationsleite angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="700a4-133">This way, you can use the Term Store Management tool in **Site Settings** to add or delete navigation terms and to manage the navigation taxonomy that is displayed by the Top Navigation snippet.</span></span>
  
    
    
<span data-ttu-id="700a4-134">In diesem Beispiel verwendet die Website die verwaltete Navigation, die obere Navigationsleiste ruft ihre Einträge also von einem Terminologiespeicher ab.</span><span class="sxs-lookup"><span data-stu-id="700a4-134">In this example, the site uses managed navigation, so the top navigation control pulls its entries from a term store.</span></span> <span data-ttu-id="700a4-135">Es gibt eine Ebene von Flyouts, die angezeigt werden, wenn Sie den Mauszeiger über einen Navigationsausdruck der obersten Ebene bewegen, z. B. **Computer**.</span><span class="sxs-lookup"><span data-stu-id="700a4-135">There is one level of flyouts that appear when you hover over a top-level navigation term, such as **Computers**.</span></span> <span data-ttu-id="700a4-136">In diesem Abschnitt wird veranschaulicht, wie diese benutzerdefinierten Formatvorlagen die SharePoint-Standardformatvorlagen überschreiben.</span><span class="sxs-lookup"><span data-stu-id="700a4-136">This section demonstrates how these custom styles override the default SharePoint styles.</span></span>
  
    
    

### <a name="sample-1-navigation-div-from-the-html-mockup-file"></a><span data-ttu-id="700a4-137">Beispiel 1: Navigation \<div\> aus der HTML-Modelldatei</span><span class="sxs-lookup"><span data-stu-id="700a4-137">Sample 1: Navigation \<div\> from the HTML mockup file</span></span>

<span data-ttu-id="700a4-138">Bevor Sie beim Entwerfen des HTML-Modells für Ihre Masterseite den Entwurfs-Manager verwenden, werden Sie wahrscheinlich HTML und CSS zum Entwerfen eines funktionalen Elements der oberen Navigationsleiste verwenden.</span><span class="sxs-lookup"><span data-stu-id="700a4-138">Before you use Design Manager, when you design the HTML mockup for your master page, you'll likely use HTML and CSS to design a functional top navigation element.</span></span> <span data-ttu-id="700a4-139">In diesem HTML-Beispiel wird eine grundlegende Struktur für die obere Navigationsleiste verwendet: ein **\<div\>**-Element mit einer ID und einem Klassennamen, eine Liste für die Einträge der oberen Navigationsleiste und eine verschachtelte Liste für jedes Flyout-Untermenü.</span><span class="sxs-lookup"><span data-stu-id="700a4-139">This HTML sample uses a basic structure for the top navigation: a **\<div\>** element with an ID and class name, a list for the top-level navigation entries, and a nested list for each flyout submenu.</span></span>
  
    
    

```HTML

<div id="navigation" class="msax-Navigation">
   <ul>
      <li><a href="#">Cameras</a>
         <ul>
            <li><a href="#">Camcorders</a></li>
            <li><a href="#">Digital cameras</a></li>
            <li><a href="#">Disposable cameras</a></li>
            <li><a href="#">Film cameras</a></li>
         </ul>
      </li>
      <li><a href="#">Computers</a>
         <ul>
            <li><a href="#">Desktops</a></li>
            <li><a href="#">Laptops</a></li>
            <li><a href="#">Netbooks</a></li>
            <li><a href="#">Tablets</a></li>
         </ul>
      </li>
      <li><a href="#">Media</a>
         <ul>
            <li><a href="#">Movies</a></li>
            <li><a href="#">Music</a></li>
            <li><a href="#">TV shows </a></li>
            <li><a href="#">Video games </a></li>
         </ul>
      </li>
      <li></li>
   </ul>
</div>

```


### <a name="sample-2-navigation-div-styled-with-custom-css"></a><span data-ttu-id="700a4-140">Beispiel 2: Navigation \<div\> formatiert mit benutzerdefiniertem CSS</span><span class="sxs-lookup"><span data-stu-id="700a4-140">Sample 2: Navigation \<div\> styled with custom CSS</span></span>

<span data-ttu-id="700a4-141">Um die SharePoint-Standardformatvorlagen zu überschreiben, fügen Sie in die HTML-Modelldatei einen Standardlink zu Ihrer CSS-Datei `(<link rel="stylesheet" type="text/css" href="URLtoYourCustomCSSFile"/>` ein, unmittelbar vor dem schließenden **\</head\>**-Tag.</span><span class="sxs-lookup"><span data-stu-id="700a4-141">To override the default SharePoint styles, in the mockup HTML file, include a standard link to your CSS file  `(<link rel="stylesheet" type="text/css" href="URLtoYourCustomCSSFile"/>`) just before the closing **\</head\>** tag.</span></span>
  
    
    
<span data-ttu-id="700a4-142">Beachten Sie in diesen HTML-und CSS-Beispielen Folgendes:</span><span class="sxs-lookup"><span data-stu-id="700a4-142">In these HTML and CSS samples, note the following:</span></span>
  
    
    

- <span data-ttu-id="700a4-143">Navigationseinträge werden mithilfe des Formats `.msax-Navigation ul li` formatiert, anstatt Klassen direkt auf die ** \<uI\>**- oder **\<li\>**-Tags anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="700a4-143">Navigation entries are styled by using the format  `.msax-Navigation ul li` instead of applying classes directly to the **\<ul\>** or **\<li\>** tags.</span></span>
    
  
- <span data-ttu-id="700a4-144">Formatvorlagen verwenden die Syntax `.msax-Navigation ul li` anstelle von `.msax-Navigation ul>li`, da das Codeausschnitt-Markup möglicherweise intervenierende **\<div\>**-Tags zwischen den ausgewählten Elementen enthält.</span><span class="sxs-lookup"><span data-stu-id="700a4-144">Styles use the syntax  `.msax-Navigation ul li` instead of `.msax-Navigation ul>li` because the snippet markup may contain intervening **\<div\>** tags between the selected elements.</span></span>
    
  
- <span data-ttu-id="700a4-145">Der HTML-Modell enthält ein leeres **\<li\>\</li\>**- Element als letzten Eintrag von **\<ul\>** auf oberster Ebene.</span><span class="sxs-lookup"><span data-stu-id="700a4-145">The HTML mockup contains an empty **\<li\>\</li\>** element as the last entry of the top-level **\<ul\>**.</span></span> <span data-ttu-id="700a4-146">Dies liegt daran, dass SharePoint bei aktivierter verwalteter Navigation den Befehl **Links bearbeiten** als letzten Eintrag für die obere Navigationsleiste hinzufügt, und die finale Website muss diese Option in der Regel nicht anzeigen.</span><span class="sxs-lookup"><span data-stu-id="700a4-146">This is because, with managed navigation turned on, SharePoint adds an **Edit Links** command as the final entry to the top-level navigation, and the final site typically does not need to display this option.</span></span> <span data-ttu-id="700a4-147">Das CSS-Beispiel verwendet `.msax-Navigation ul li:last-child`, um diesen Eintrag auszuwählen und den Anzeigewert auf `none` festzulegen.</span><span class="sxs-lookup"><span data-stu-id="700a4-147">The CSS sample uses `.msax-Navigation ul li:last-child` to select this entry and set the display value to `none`.</span></span> <span data-ttu-id="700a4-148">Das leere **\<li\>\</li\>**-Element in der HTML-Datei ist ein temporärer Ersatz für den standardmäßigen Eintrag **Links bearbeiten**.</span><span class="sxs-lookup"><span data-stu-id="700a4-148">The empty **\<li\>\</li\>** element in the HTML file is a temporary substitute for the default **Edit Links** entry.</span></span> <span data-ttu-id="700a4-149">Beachten Sie dieses finale **\<li\>**-Element, wenn Ihre Website die verwaltete Navigation und CSS `li:last-child`-Selektoren verwendet.</span><span class="sxs-lookup"><span data-stu-id="700a4-149">Be aware of this final **\<li\>** element if your site uses managed navigation and your CSS uses any `li:last-child` selectors.</span></span>
    
  



```HTML

.msax-Navigation {
margin: 10px 0px; top: 0px; position: relative;
z-index:200;
}
.msax-Navigation a {
margin: 0px; padding: 0px; border: 0px currentColor;
}
.msax-Navigation ul {
list-style: none; margin: 0px; padding: 0px; font-size: 16px; z-index:200;
}
.msax-Navigation ul li {
padding: 10px; display: inline-block; position: relative; z-index:200;
}
.msax-Navigation ul li:first-child {
margin: 0px;
}
.msax-Navigation ul li:last-child {
margin: 0px; padding: 0px; display: none;
}
.msax-Navigation ul li a.selected, .msax-Navigation ul li.selected {
background-color: rgb(58,60,62) !important;
color:rgb(255,255,255) !important;
}
.msax-Navigation ul li a {
width: 100%; color: rgb(58,60,62); font-size: 16px;
}
.msax-Navigation ul li:hover {
background-color: rgb(58,60,62);
color:rgb(255,255,255) !important;
}
.msax-Navigation ul li a:hover {
text-decoration: none;
color:rgb(255,255,255) !important;
}
.msax-Navigation li ul {
left: 0px; top: 35px; display: none; position: absolute; min-width: 100px; box-shadow: 5px 5px 10px 0px rgb(0,0,0); background-color: rgb(58,60,62);
}
.msax-Navigation li:hover ul {
display: block; z-index: 150;
}
.msax-Navigation li li {
margin: 0px; padding: 5px 10px 5px 0px; border-top-width: 0px; display: block; min-width: 100px;
}
.msax-Navigation li li:last-child {
margin: 0px; padding: 5px 10px 5px 0px; border-top-width: 0px; display: block; min-width: 100px;
}
.msax-Navigation li li a {
width: 100%; padding-left: 10px; display: block; color:rgb(255,255,255) !important;
}
.msax-Navigation li li:hover {
background-color: rgb(120, 120, 120);
}

```


### <a name="sample-3-read-only-preview-of-the-top-navigation-snippet"></a><span data-ttu-id="700a4-150">Beispiel 3: Schreibgeschützte Vorschau des Codeausschnitts der oberen Navigationsleiste</span><span class="sxs-lookup"><span data-stu-id="700a4-150">Sample 3: Read-only preview of the top navigation snippet</span></span>

<span data-ttu-id="700a4-151">Nachdem Ihre benutzerdefinierten Formatvorlagen im HTML-Modell implementiert wurden und Sie über ein funktionales Element der oberen Navigationsleiste verfügen, führen Sie die üblichen Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="700a4-151">After your custom styles are implemented in your HTML mockup and you have a functional top navigation element, follow the usual steps:</span></span>
  
    
    

1. <span data-ttu-id="700a4-152">Ordnen Sie ein Netzlaufwerk zu.</span><span class="sxs-lookup"><span data-stu-id="700a4-152">Map a network drive.</span></span>
    
  
2. <span data-ttu-id="700a4-153">Laden Sie Ihre Designdateien hoch.</span><span class="sxs-lookup"><span data-stu-id="700a4-153">Upload your design files.</span></span>
    
  
3. <span data-ttu-id="700a4-154">Konvertieren Sie die HTML-Datei in eine Masterseite.</span><span class="sxs-lookup"><span data-stu-id="700a4-154">Convert the HTML file into a master page.</span></span>
    
  
4. <span data-ttu-id="700a4-155">Zeigen Sie Probleme in der Vorschau an, und korrigieren Sie sie.</span><span class="sxs-lookup"><span data-stu-id="700a4-155">Preview and fix any issues.</span></span>
    
  
5. <span data-ttu-id="700a4-156">Fügen Sie den Codeausschnitt der oberen Navigationsleiste in die HTML-Masterseite mithilfe des Codeausschnittkatalog ein.</span><span class="sxs-lookup"><span data-stu-id="700a4-156">Add the top navigation snippet to the HTML master page by using the Snippet Gallery.</span></span>
    
  
<span data-ttu-id="700a4-157">Beachten Sie im Codeausschnittkatalog Folgendes, wenn Sie die Eigenschaften des Codeausschnitts der oberen Navigationsleiste konfigurieren:</span><span class="sxs-lookup"><span data-stu-id="700a4-157">In the Snippet Gallery, when you configure the properties of the top navigation snippet, note the following:</span></span>
  
    
    

- <span data-ttu-id="700a4-158">Nehmen Sie im Bereich **Wichtig** am oberen Rand keine Änderungen an der **CssClass**-Eigenschaft vor.</span><span class="sxs-lookup"><span data-stu-id="700a4-158">In the **Important** section at the top, do not make any changes to the **CssClass** property.</span></span>
    
  
- <span data-ttu-id="700a4-159">Nehmen Sie keine Änderungen an Eigenschaften unter der Überschrift **AjaxDelta** vor, da diese Eigenschaften im Zusammenhang mit den MDS-Eigenschaften stehen, die SharePoint verwendet, um den HTML-Codeausschnitt in den entsprechenden ASP.NET-Codeausschnitt zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="700a4-159">Do not make any changes to properties under the **AjaxDelta** heading because these properties are related to the MDS properties that SharePoint uses to convert the HTML snippet into the corresponding ASP.NET snippet.</span></span> <span data-ttu-id="700a4-160">Dies gilt für alle Codeausschnitte, nicht nur für den Codeausschnitt der oberen Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="700a4-160">This applies to any snippet, not just the top navigation snippet.</span></span>
    
  
- <span data-ttu-id="700a4-161">Wenn Sie beabsichtigen, die SharePoint-Standardformatvorlagen zu überschreiben, legen Sie Codeausschnittkatalog im Abschnitt **Behavior** unter **AspMenu** (wenn der Codeausschnitt mehrere Steuerelemente enthält, z. B. ein delegate-Steuerelement, sind möglicherweise mehrere Abschnitte **Behavior** vorhanden) die Option **ClientIDMode** auf **Static**.</span><span class="sxs-lookup"><span data-stu-id="700a4-161">If you're planning to override the default SharePoint styles, in the Snippet Gallery, in the **Behavior** section under **AspMenu** (there may be more than one **Behavior** section if the snippet contains more than one control, such as a delegate control), set **ClientIDMode** to **Static**.</span></span> <span data-ttu-id="700a4-162">Wenn Sie die Option **ClientIDMode** auf die Standardeinstellung **Inherit** festgelegt lassen, ändern sich die angewendeten CSS-Klassen des Codeausschnitts basierend auf der Sortierung der Codeausschnitte auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="700a4-162">If you leave **ClientIDMode** set to the default setting, **Inherit**, the snippet's applied CSS classes will change based on the ordering of snippets on the page.</span></span> <span data-ttu-id="700a4-163">Weitere Informationen zu **ClientIDMode** finden Sie unter [Control.ClientIDMode-Eigenschaft]((http://msdn.microsoft.com/de-DE/library/system.web.ui.control.clientidmode.aspx)).</span><span class="sxs-lookup"><span data-stu-id="700a4-163">For more information about **ClientIDMode**, see  [Control.ClientIDMode property]((http://msdn.microsoft.com/de-DE/library/system.web.ui.control.clientidmode.aspx)).</span></span>
    
    <span data-ttu-id="700a4-164">Standardmäßig verwendet das Steuerelement der oberen Navigationsleiste beispielsweise standardmäßige SharePoint-ID-Attribute wie **zz5_TopNavigationMenu** und **zz6_RootAspMenu**.</span><span class="sxs-lookup"><span data-stu-id="700a4-164">For example, by default, the top navigation control uses default SharePoint ID attributes such as **zz5_TopNavigationMenu** and **zz6_RootAspMenu**.</span></span> <span data-ttu-id="700a4-165">Durch Ändern von **ClientIDMode** in **Static** ermöglichen Sie die Verwendung dieser Standard-IDs als Selektoren in Ihrer eigenen CSS, um die SharePoint-Standardformatvorlagen zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="700a4-165">By changing **ClientIDMode** to **Static**, you make it possible to use these default IDs as selectors in your own CSS to override the default SharePoint styles.</span></span>
    
  
- <span data-ttu-id="700a4-166">Einige Eigenschaften sind bereits so konfiguriert, dass das Branding des Codeausschnitts der oberen Navigationsleiste vereinfacht wird, indem die standardmäßigen Verhaltensweisen von dynamischem CSS und JavaScript eliminiert werden. **UseSimpleRendering** wird beispielsweise standardmäßig auf **True** festgelegt, und **MaximumDynamicDisplayLevels** wird auf **0** festgelegt.</span><span class="sxs-lookup"><span data-stu-id="700a4-166">Some properties are already configured to make branding the top navigation snippet easier by eliminating the default dynamic CSS and JavaScript behaviors—for example, by default **UseSimpleRendering** is set to **True** and **MaximumDynamicDisplayLevels** is set to **0**.</span></span> <span data-ttu-id="700a4-167">Weitere Informationen zu bestimmten Eigenschaften des Codeausschnitts der oberen Navigationsleiste finden Sie unter [AspMenu-Eigenschaften]((http://msdn.microsoft.com/de-DE/library/ms412476.aspx)) und [Menu-Eigenschaften]((http://msdn.microsoft.com/de-DE/library/282668a1.aspx)).</span><span class="sxs-lookup"><span data-stu-id="700a4-167">For more information about specific properties of the top navigation snippet, see  [AspMenu properties]((http://msdn.microsoft.com/de-DE/library/ms412476.aspx)) and [Menu properties]((http://msdn.microsoft.com/de-DE/library/282668a1.aspx)).</span></span>
    
  
<span data-ttu-id="700a4-168">Nachdem Sie den Codeausschnitt der oberen Navigationsleiste im Codeausschnittkatalog konfiguriert haben, wählen Sie **Aktualisieren** und dann **In die Zwischenablage kopieren** aus.</span><span class="sxs-lookup"><span data-stu-id="700a4-168">After you configure the top navigation snippet in the Snippet Gallery, choose **Update**, and then choose **Copy to Clipboard**.</span></span> <span data-ttu-id="700a4-169">Löschen Sie auf der HTML-Masterseite den Inhalt der Navigation `<div id="navigation" class="msax-Navigation">`, die das Modellsteuerelement enthält (löschen Sie nur den Inhalt des **\<div\>**-Tags und nicht das **\<div\>**-Tag selbst), und kopieren Sie dann den Codeausschnitt in die Navigation **\<div\>**.</span><span class="sxs-lookup"><span data-stu-id="700a4-169">In the HTML master page, delete the contents of the navigation  `<div id="navigation" class="msax-Navigation">` that contains your mockup control (delete just the contents of the **\<div\>** tag, not the **\<div\>** tag itself), and then copy the snippet into the navigation **\<div\>**.</span></span> <span data-ttu-id="700a4-170">Ändern Sie, falls erforderlich, die Position der **\<#div\>**-Navigation, in der Regel direkt nach Beginn des `<div id="s4-bodyContainer">`-Tags, jedoch vor dem **\<#div\>** mit `PlaceHolderMain`.</span><span class="sxs-lookup"><span data-stu-id="700a4-170">If necessary, reposition the navigation **\<div\>**, typically just after the start of the  `<div id="s4-bodyContainer">` tag but before the **\<div\>** containing `PlaceHolderMain`.</span></span>
  
    
    
<span data-ttu-id="700a4-171">Für einen einfachen Vergleich mit dem HTML-Code der **\<#div\>**-Navigation oben, enthält das folgende Beispiel den **\<div\>**-Teil der Navigation des Codeausschnitts der oberen Navigationsleiste.</span><span class="sxs-lookup"><span data-stu-id="700a4-171">For easy comparison with the HTML of the navigation **\<div\>** above, the following sample contains the navigation **\<div\>** portion of the top navigation snippet.</span></span> <span data-ttu-id="700a4-172">Beachten Sie, dass dies nicht der gesamte Codeausschnitt ist.</span><span class="sxs-lookup"><span data-stu-id="700a4-172">Note that this is not the entire snippet.</span></span>
  
    
    



```HTML

<div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox">
     <ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static">
          <li class="static">
          <a accesskey="1" class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Cameras</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/camcorders" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Camcorders</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/digital-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Digital cameras</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/disposable-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Disposable cameras</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/cameras/film-cameras" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Film cameras</span></span></a></li>
          </ul>
          </li>
          <li class="static">
          <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Computers</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/desktops" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Desktops</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/laptops" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Laptops</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/netbooks" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Netbooks</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/computers/tablets" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Tablets</span></span></a></li>
          </ul>
          </li>
          <li class="static">
          <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media" tabindex="0">
          <span class="additional-background ms-navedit-flyoutArrow">
          <span class="menu-item-text">Media</span></span></a><ul class="static">
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/movies" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Movies</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/music" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Music</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/tv-shows" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">TV shows</span></span></a></li>
               <li class="static">
               <a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" href="/sites/PubSite/media/video-games" tabindex="0">
               <span class="additional-background ms-navedit-flyoutArrow">
               <span class="menu-item-text">Video games</span></span></a></li>
          </ul>
          </li>
          <li class="static ms-verticalAlignTop ms-listMenu-editLink ms-navedit-editArea">
          <span id="zz7_TopNavigationMenu_NavMenu_Edit" class="ms-navedit-editSpan">
          <a id="zz7_TopNavigationMenu_NavMenu_EditLinks" class="ms-navedit-editLinksText" href="#" onclick="g_QuickLaunchMenu = null; EnsureScriptParams('quicklaunch.js', 'QuickLaunchInitEditMode', 'zz7_TopNavigationMenu', 2, 0, 0, ''); cancelDefault(event); return false;">
          <span class="ms-displayInlineBlock">
          <span class="ms-navedit-editLinksIconWrapper ms-verticalAlignMiddle">
          <img class="ms-navedit-editLinksIcon" src="/_layouts/15/images/spcommon.png?rev=23" /></span><span class="ms-metadata ms-verticalAlignMiddle">Edit Links</span></span></a><span id="zz7_TopNavigationMenu_NavMenu_Loading" class="ms-navedit-menuLoading ms-hide"><a id="zz7_TopNavigationMenu_NavMenu_GearsLink" href="#" onclick="HideGears(); return false;" title="This animation indicates the operation is in progress. Click to remove this animated image."><img id="zz7_TopNavigationMenu_NavMenu_GearsImage" src="/_layouts/15/images/loadingcirclests16.gif?rev=23" /></a></span><div id="zz7_TopNavigationMenu_NavMenu_ErrorMsg" class="ms-navedit-errorMsg">
          </div>
          </span></li>
     </ul>
</div>

```

<span data-ttu-id="700a4-173">Anstatt nur benutzerdefinierte Formatvorlagen zu verwenden, kann es möglicherweise ein Szenario geben, in dem Sie nur eine bestimmte Formatvorlage überschreiben möchten.</span><span class="sxs-lookup"><span data-stu-id="700a4-173">Instead of using only custom styles, you may have a scenario where you want to override just a specific style.</span></span> <span data-ttu-id="700a4-174">Um beispielsweise den Knoten **Links bearbeiten** auszublenden, können Sie eine benutzerdefinierte Formatvorlage erstellen, die die Standard-ID **zz7_TopNavigationMenu_NavMenu_Edit** verwendet, um die Anzeigeeinstellung auf `none` festzulegen.</span><span class="sxs-lookup"><span data-stu-id="700a4-174">For example, to hide the **Edit Links** node, you can create a custom style that uses the default id **zz7_TopNavigationMenu_NavMenu_Edit** to set the display setting to `none`.</span></span>
  
    
    

## <a name="see-also"></a><span data-ttu-id="700a4-175">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="700a4-175">See also</span></span>
<span data-ttu-id="700a4-176"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="700a4-176"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="700a4-177">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="700a4-177">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="700a4-178">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="700a4-178">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="700a4-179">Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint</span><span class="sxs-lookup"><span data-stu-id="700a4-179">How to: Convert an HTML file into a master page in SharePoint</span></span>](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="700a4-180">Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="700a4-180">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="700a4-181">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="700a4-181">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

