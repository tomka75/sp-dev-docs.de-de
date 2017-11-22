---
title: "Übersicht über den Entwurfs-Manager in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 29834b3f-3815-4347-91d3-296387663114
ms.openlocfilehash: 6422ff4e19136bac523e1a4d59100241091ae11b
ms.sourcegitcommit: 11d9185437fc819ab41421c0f4fe06aa300b9d28
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/25/2017
---
# <a name="overview-of-design-manager-in-sharepoint"></a><span data-ttu-id="eb423-102">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="eb423-102">Overview of Design Manager in SharePoint</span></span>
<span data-ttu-id="eb423-103">In diesem Artikel erfahren Sie, wie Sie den Entwurfs-Manager zum Branding von SharePoint-Websites verwenden können.</span><span class="sxs-lookup"><span data-stu-id="eb423-103">Get an overview of using Design Manager to brand your SharePoint site.</span></span> <span data-ttu-id="eb423-104">Der Entwurfs-Manager ist ein Veröffentlichungsfeature, das auf Veröffentlichungswebsites in SharePoint und Office 365 verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="eb423-104">Overview of Design Manager in SharePoint : Get an overview of using Design Manager to brand your SharePoint site. Design Manager is a publishing feature that is available in publishing sites in both SharePoint Server 2013 and Office 365.</span></span> 
## <a name="introduction-to-design-manager"></a><span data-ttu-id="eb423-105">Einführung in den Entwurfs-Manager</span><span class="sxs-lookup"><span data-stu-id="eb423-105">Introduction to Design Manager</span></span>
<span data-ttu-id="eb423-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="eb423-106"></span></span>

<span data-ttu-id="eb423-107">Ihre SharePoint-Website soll Ihre Marke repräsentieren und nicht „wie SharePoint“ aussehen? Mit einem benutzerdefinierten Design und Entwurfs-Manager können Sie das sicherstellen.</span><span class="sxs-lookup"><span data-stu-id="eb423-107">If you want your SharePoint site to represent your organization's brand and not "look like SharePoint," you can create a custom design and use Design Manager to achieve that goal.</span></span> <span data-ttu-id="eb423-108">Der Entwurfs-Manager ist ein Feature in SharePoint und macht es einfacher, vollständig individuell angepasste, pixelgenaue Designs zu erstellen, mit den Ihnen bereits vertrauten Webdesigntools.</span><span class="sxs-lookup"><span data-stu-id="eb423-108">Design Manager is a feature in sp15allshort that makes it easier to create a fully customized, pixel-perfect design while using the web-design tools that you're already familiar with. Design Manager is a publishing feature that is available in publishing sites in both sps15short and off365short. You can also use Design Manager to brand the public-facing website in off365short.</span></span> <span data-ttu-id="eb423-109">Der Entwurfs-Manager ist ein Veröffentlichungsfeature, das auf Veröffentlichungswebsites in SharePoint und Office 365 verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="eb423-109">Overview of Design Manager in SharePoint : Get an overview of using Design Manager to brand your SharePoint site. Design Manager is a publishing feature that is available in publishing sites in both SharePoint Server 2013 and Office 365.</span></span> 
  
    
    
<span data-ttu-id="eb423-p103">Mit dem Entwurfs-Manager können Sie mithilfe eines beliebigen Webdesigntools oder eines von Ihnen bevorzugten HTML-Editors nur mit HTML und CSS ein visuelles Design für Ihre Website erstellen und dieses Design dann in SharePoint hochladen. Der Entwurfs-Manager ist die zentrale Schnittstelle, über die Sie sämtliche Aspekte eines benutzerdefinierten Designs verwalten.</span><span class="sxs-lookup"><span data-stu-id="eb423-p103">With Design Manager, you can create a visual design for your website by using whatever web design tool or HTML editor you prefer, using only HTML and CSS, and then upload that design into SharePoint. Design Manager is the central hub and interface where you manage all aspects of a custom design.</span></span>
  
    
    
<span data-ttu-id="eb423-p104">Die Erstellung des visuellen Designs einer Websites erfolgt häufig im Rahmen eines umfangreicheren Prozesses, an dem mehrere Personen oder Organisationen beteiligt sind. Eine allgemeinere Übersicht über die Aufgaben finden Sie unter  [Design und Branding in SharePoint](http://go.microsoft.com/fwlink/?LinkId=262838)</span><span class="sxs-lookup"><span data-stu-id="eb423-p104">Creating the visual design of a site often fits into a larger process, in which multiple people or organizations are involved. For a roadmap of the tasks from a larger perspective, see  [Design and branding in SharePoint](http://go.microsoft.com/fwlink/?LinkId=262838)</span></span>
  
    
    
<span data-ttu-id="eb423-114">Im Allgemeinen führt der Webdesigner die folgenden Aufgaben durch:</span><span class="sxs-lookup"><span data-stu-id="eb423-114">At a high level, the designer will perform the following tasks:</span></span>
  
    
    

- <span data-ttu-id="eb423-p105">Verstehen der wesentlichen SharePoint-Designkonzepte. Weitere Informationen finden Sie unter  [Übersicht über das SharePoint-Seitenmodell](overview-of-the-sharepoint-page-model.md).</span><span class="sxs-lookup"><span data-stu-id="eb423-p105">Understand core SharePoint design concepts. For more information, see  [Overview of the SharePoint page model](overview-of-the-sharepoint-page-model.md).</span></span>
    
  
- <span data-ttu-id="eb423-p106">Erstellen eines Modells des Designs in HTML and CSS. Die Designerstellung ist eine zentrale Kompetenz eines Webdesigners und wird in diesem Artikel nicht behandelt.</span><span class="sxs-lookup"><span data-stu-id="eb423-p106">Create a mock-up of the design in HTML and CSS. Creating the design is a core skill of a web designer, and is not covered in this article.</span></span>
    
  
- <span data-ttu-id="eb423-p107">Implementieren des Designs mithilfe des Entwurfs-Managers. Abschnitte dieses Artikels bieten eine Einführung zum Entwurfs-Manager und den Prozess der Verwendung des Entwurfs-Managers zum Implementieren eines visuellen Designs.</span><span class="sxs-lookup"><span data-stu-id="eb423-p107">Implement the design by using Design Manager. Sections of this article provide an introduction to Design Manager and the process of using Design Manager to implement a visual design.</span></span>
    
 


## <a name="use-design-manager-to-implement-a-design"></a><span data-ttu-id="eb423-121">Implementieren eines Designs mit dem Entwurfs-Manager</span><span class="sxs-lookup"><span data-stu-id="eb423-121">Use Design Manager to implement a design</span></span>
<span data-ttu-id="eb423-122"><a name="Use"> </a></span><span class="sxs-lookup"><span data-stu-id="eb423-122"></span></span>

<span data-ttu-id="eb423-p108">Wenn Sie den Entwurfs-Manager öffnen, sehen Sie auf der linken Seite eine Reihe von Links, welche die allgemeinen Aufgaben darstellen, die Sie durchführen müssen. Je nach Ihrem Design und den Anforderungen Ihrer Website müssen Sie möglicherweise nicht alle diese Aufgaben durchführen, und Sie müssen sie nicht unbedingt in dieser Reihenfolge durchführen. Diese Abfolge ist dennoch ein hilfreicher Ausgangspunkt.</span><span class="sxs-lookup"><span data-stu-id="eb423-p108">When you look at Design Manager, you see a series of links on the left side that represent the high-level tasks that you have to perform. Depending on your design and your site's requirements, you may not have to perform all of these tasks, and you don't necessarily have to perform them in this order. Still, this sequence is a useful starting point.</span></span>
  
    
    

### <a name="before-you-begin"></a><span data-ttu-id="eb423-126">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="eb423-126">Before you begin</span></span>

<span data-ttu-id="eb423-p109">Bevor Sie den Entwurfs-Manager verwenden können, benötigen Sie ein Design. Sie können Ihr eigenes erstellen oder eine fertige Websitevorlage verwenden. Ein "Design" ist einfach eine Gruppe von Dateien, die das visuelle Design Ihrer Website implementieren. Diese Gruppe umfasst i. d. R. Folgendes:</span><span class="sxs-lookup"><span data-stu-id="eb423-p109">Before you can use Design Manager, you need a design. You can create your own, or use a ready-made website template. A "design" is simply a group of files that implement the visual design of your site, most commonly:</span></span>
  
    
    

- <span data-ttu-id="eb423-130">Mindestens eine HTML-Datei, die in eine SharePoint-Gestaltungsvorlage umgewandelt wird</span><span class="sxs-lookup"><span data-stu-id="eb423-130">At least one HTML file that will be converted into a SharePoint master page</span></span>
    
  
- <span data-ttu-id="eb423-131">Eine oder mehrere CSS-Dateien</span><span class="sxs-lookup"><span data-stu-id="eb423-131">One or more CSS files</span></span>
    
  
- <span data-ttu-id="eb423-132">JavaScript-Dateien</span><span class="sxs-lookup"><span data-stu-id="eb423-132">JavaScript files</span></span>
    
  
- <span data-ttu-id="eb423-133">Bilder</span><span class="sxs-lookup"><span data-stu-id="eb423-133">Images</span></span>
    
  
- <span data-ttu-id="eb423-134">Andere unterstützende Dateien</span><span class="sxs-lookup"><span data-stu-id="eb423-134">Other supporting files</span></span>
    
  
<span data-ttu-id="eb423-p110">Wenn Sie Ihre Website in HTML und CSS modellieren, haben Sie wahrscheinlich mehrere HTML-Dateien, die Designs dafür implementieren, wie verschiedene Seiten oder Typen von Seiten angezeigt werden sollen. Bedenken Sie, dass nur eine dieser HTML-Dateien in die Gestaltungsvorlage konvertiert wird (es sein denn, Sie haben mehrere Gerätekanäle, wobei jeder Kanal über eine eigene Gestaltungsvorlage verfügt – siehe folgender Abschnitt). Nachdem Sie den Entwurfs-Manager zum Erstellen anderer Websiteelemente wie Seitenlayouts oder Anzeigevorlagen verwendet haben, können Sie Markup von Ihren HTML-Modellen in die HTML- und CSS-Dateien übertragen, die mit der Gestaltungs- oder Anzeigevorlage verknüpft sind.</span><span class="sxs-lookup"><span data-stu-id="eb423-p110">As you mock up your site in HTML and CSS, you will likely have several HTML files that implement designs for how you want different pages or types of pages to appear. Remember that only one of these HTML files will be converted into the master page (unless you have multiple device channels, where each channel has its own master page—see the following section). After you use Design Manager to create other site elements, such as page layouts or display templates, you can transfer markup from your HTML mock-ups to the HTML and CSS files associated with the page layout or display template.</span></span>
  
    
    
<span data-ttu-id="eb423-p111">Bevor Sie beginnen, benötigen Sie auch die erforderlichen SharePoint-Berechtigungen. Um den Entwurfs-Manager zu verwenden, benötigen Sie mindestens die Designer-Berechtigungsstufe.</span><span class="sxs-lookup"><span data-stu-id="eb423-p111">Before you begin, you also need the required SharePoint permissions. To use Design Manager, you must have at least the Designer permission level.</span></span>
  
    
    

### <a name="manage-device-channels"></a><span data-ttu-id="eb423-140">Verwalten von Gerätekanälen</span><span class="sxs-lookup"><span data-stu-id="eb423-140">Manage device channels</span></span>

<span data-ttu-id="eb423-p112">Bereits bevor Sie Ihre Website entwerfen, sollten Sie bedenken, auf welche Geräte Ihre Website ausgelegt sein soll, und wie die Benutzererfahrung auf jedem Gerät aussehen soll. So möchten Sie das Design Ihrer Website vielleicht für eine bestimmte Klasse von Smartphones oder Tablet-PCs optimieren.</span><span class="sxs-lookup"><span data-stu-id="eb423-p112">Even before you design your site, you want to consider what devices your site should target and what will be the user experience on each device. For example, you may want to optimize your site's design for a certain class of smart phones or tablets.</span></span>
  
    
    
<span data-ttu-id="eb423-p113">Je nachdem, welche Kanäle Sie definieren, möchten Sie vielleicht mehrere Designs und damit mehrere HTML-Dateien verwenden, wobei jede Datei in eine eigene Gestaltungsvorlage konvertiert wird. Außerdem kann jede HTML-Datei (und somit jede Gestaltungsvorlage) ihre eigene CSS-Datei referenzieren. Gerätekanäle sollten gleich am Anfang, bevor Sie mit dem Entwerfen Ihrer Website beginnen, berücksichtigt werden.</span><span class="sxs-lookup"><span data-stu-id="eb423-p113">Depending on what channels you define, you may want several designs, and so several HTML files, where each file gets converted into a separate master page. Also, each HTML file (and so each master page) can reference its own CSS file. Before you design your site, device channels are one of the first things to consider.</span></span>
  
    
    
<span data-ttu-id="eb423-p114">Mit Gerätekanälen können Sie eine einzelne Veröffentlichungswebsite auf verschiedene Weise rendern, indem Sie unterschiedlichen Geräten unterschiedliche Designs zuordnen. Jeder Kanal kann seine eigene Gestaltungsvorlage besitzen, die mit einem Stylesheet verknüpft ist, das für ein bestimmtes Gerät optimiert ist. Jeder Kanal gibt die Benutzer-Agent-Unterzeichenfolge für ein oder mehrere Geräte an, wie z. B. "Windows Phone OS". Dies sind Regeln, die festlegen, welche Geräte in jeden Kanal eingeschlossen werden. Wenn Besucher dann zu Ihrer Website navigieren, erfasst jeder Kanal den Datenverkehr für das entsprechende Gerät oder die entsprechende Geräteklasse, wie z. B. Windows Phones, und Besuchern wird Ihre Website in einem für ihr jeweiliges Gerät optimierten Design angezeigt.</span><span class="sxs-lookup"><span data-stu-id="eb423-p114">With device channels, you can render a single publishing site in multiple ways by mapping different designs to different devices. Each channel can have its own master page that links to a style sheet that is optimized for a specific device. Each channel specifies the user agent substrings for one or more devices, such as "Windows Phone OS". These are rules that determine what devices are included in each channel. Then, when visitors browse your site, each channel captures the traffic for its specified device or class of devices, such as Windows phones, and visitors see your site in a design optimized for their specific device.</span></span>
  
    
    
<span data-ttu-id="eb423-p115">Gerätekanäle werden in einer SharePoint-Liste erstellt und gespeichert, in der die Reihenfolge eine Rolle spielt, da Gerätekanäle auch Ranglisten haben. Gerätekanäle sind in der Liste von oben nach unten geordnet, und die Einschlussregeln werden in dieser Reihenfolge verarbeitet. Das bedeutet, dass Gerätekanäle mit den spezifischsten Regeln an oberster Stelle stehen sollten. So sollte etwa ein Kanal, der auf "Windows Phone OS 7.0" ausgelegt ist, über einem Kanal stehen, der auf "Windows Phone OS" ausgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="eb423-p115">Device channels are created and stored in a SharePoint list in which order matters, because device channels also have rankings. Device channels in the list are ordered from top to bottom, and the inclusion rules are processed in that order. This means that you want device channels with the most specific rules at the top. For example, a channel targeting "Windows Phone OS 7.0" should precede a channel targeting "Windows Phone OS".</span></span>
  
    
    

### <a name="upload-design-files"></a><span data-ttu-id="eb423-155">Hochladen von Designdateien</span><span class="sxs-lookup"><span data-stu-id="eb423-155">Upload design files</span></span>

<span data-ttu-id="eb423-p116">Wenn Sie ein Design erstellen, können Sie einen beliebigen HTML-Editor verwenden und mit Dateien lokal auf Ihrem Computer arbeiten. Sie müssen diese Dateien aber letztendlich in die Gestaltungsvorlagengalerie Ihrer SharePoint-Website hochladen, sodass Sie Ihr Design mithilfe des Entwurfs-Managers konvertieren, in der Vorschau anzeigen und optimieren können.</span><span class="sxs-lookup"><span data-stu-id="eb423-p116">When you create a design, you can use whatever HTML editor you prefer and work with files locally on your computer. But, eventually, you will have to upload those files to the Master Page Gallery of your SharePoint site, so that you can use Design Manager to convert, preview, and polish your design.</span></span>
  
    
    
<span data-ttu-id="eb423-p117">Der einfachste Weg, Designdateien hochzuladen und weiter daran zu arbeiten, ist, der Gestaltungsvorlagengalerie Ihrer SharePoint-Website ein Laufwerk auf Ihrem Computer zuzuordnen. Dadurch wird ein Ordner auf Ihrem Computer mit der Gestaltungsvorlagengalerie verbunden, sodass Sie an Dateien arbeiten können, die sich auf dem Server in SharePoint befinden, als ob es sich um lokale Dateien handeln würde.</span><span class="sxs-lookup"><span data-stu-id="eb423-p117">The easiest way to upload and continue to work on design files is to map a drive on your computer to the Master Page Gallery of your SharePoint site. This connects a folder on your computer to the Master Page Gallery, so that you can work on files that reside on the server in SharePoint as if they were local files.</span></span>
  
    
    
<span data-ttu-id="eb423-p118">Nachdem Sie ein Netzwerklaufwerk zugeordnet haben, können Sie Ihr Design in SharePoint hochladen, indem Sie die Designdateien einfach in einen Ordner auf dem zugeordneten Laufwerk Ihres Computers hochladen, der mit SharePoint verbunden ist. Nachdem Sie Ihre HTML-Datei in eine SharePoint-Gestaltungsvorlage konvertiert und Seitenlayouts und Anzeigevorlagen erstellt haben, die jeweils eine eigene zugeordnete HTML-Datei aufweisen, können Sie diese zugeordneten HTML-Dateien in Ihrem HTML-Editor auf Ihrem Computer weiter bearbeiten. Immer wenn Sie eine Datei im zugeordneten Laufwerk speichern, synchronisiert SharePoint die Dateien auf Ihrem Computer automatisch mit der Gestaltungsvorlagengalerie. Sie können auf dem zugeordneten Laufwerk Ihre eigene Ordnerstruktur erstellen, und diese Struktur wird von SharePoint aufrechterhalten und in der Gestaltungsvorlagengalerie angezeigt. Sie sollten alle Dateien, die sich auf ein Design beziehen, in einem einzelnen Ordner ablegen und diesen Ordner dann auf das zugeordnete Laufwerk kopieren, wenn Sie bereit sind, Ihr Design hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="eb423-p118">After you map a network drive, you can upload your design to SharePoint simply by copying the design files to a folder on the mapped drive of your computer that is connected to SharePoint. After you convert your HTML file to a SharePoint master page, and after you create page layouts and display templates that each have their own associated HTML file, you can continue to edit those associated HTML files in your HTML editor on your computer. Each time you save a file in the mapped drive, SharePoint automatically synchronizes the files on your computer with the Master Page Gallery. You can create your own folder structure on the mapped drive, and that structure is maintained by SharePoint and appears in the Master Page Gallery. You should keep all files related to one design in a single folder, and then copy that folder to the mapped drive when you are ready to upload your design.</span></span>
  
    
    
<span data-ttu-id="eb423-165">Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="eb423-165">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
  
    
    

### <a name="edit-master-pages"></a><span data-ttu-id="eb423-166">Bearbeiten von Gestaltungsvorlagen</span><span class="sxs-lookup"><span data-stu-id="eb423-166">Edit master pages</span></span>

<span data-ttu-id="eb423-167">Die Erstellung einer Gestaltungsvorlage mit vollständigem Branding, die alle von Ihnen gewünschten SharePoint-Funktionen wie Navigation und Suche enthält, umfasst im Wesentlichen drei Schritte:</span><span class="sxs-lookup"><span data-stu-id="eb423-167">Creating a fully branded master page that contains all of the SharePoint functionality that you want, such as navigation and search, is basically a three-step process:</span></span>
  
    
    

1. <span data-ttu-id="eb423-168">Konvertieren einer HTML-Datei in eine SharePoint-Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="eb423-168">Convert an HTML file into a SharePoint master page.</span></span>
    
  
2. <span data-ttu-id="eb423-169">Anzeigen der Gestaltungsvorlage in der Vorschau und Beheben etwaiger Probleme</span><span class="sxs-lookup"><span data-stu-id="eb423-169">Preview the master page and fix any issues.</span></span>
    
  
3. <span data-ttu-id="eb423-170">Hinzufügen von SharePoint-Ausschnitten zur Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="eb423-170">Add SharePoint snippets to the master page.</span></span>
    
  
<span data-ttu-id="eb423-171">Jeder dieser drei Schritte wird auf einer anderen Seite im Entwurfs-Manager durchgeführt.</span><span class="sxs-lookup"><span data-stu-id="eb423-171">Each of these three steps is performed on a different page in Design Manager.</span></span>
  
    
    

#### <a name="convert-an-html-file"></a><span data-ttu-id="eb423-172">Konvertieren einer HTML-Datei</span><span class="sxs-lookup"><span data-stu-id="eb423-172">Convert an HTML file</span></span>

<span data-ttu-id="eb423-p119">Das wichtigste Feature des Entwurfs-Managers ist, dass er Ihr HTML-Design in eine SharePoint-Gestaltungsvorlage konvertiert. Damit das Design erfolgreich gerendert wird, muss eine SharePoint-Gestaltungsvorlage viele ASP.NET- und SharePoint-spezifische Elemente enthalten. Wenn Sie eine HTML-Datei in eine Gestaltungsvorlage konvertieren, erstellt der Entwurfs-Manager eine .master-Datei, die all diese erforderlichen Elemente enthält, sodass Sie diese nicht kennen müssen. Bei der Konvertierung wird Ihrer ursprünglichen HTML-Datei auch HTML-Markup (wie Kommentare) hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="eb423-p119">The core feature of Design Manager is that it converts your HTML design into a SharePoint master page. To render successfully, a SharePoint master page must contain many ASP.NET elements and elements that are specific to SharePoint. When you convert an HTML file to a master page, Design Manager creates a .master file that contains all of these required elements, so that you don't have to know about them. During conversion, some HTML markup (such as comments) also gets added to your original HTML file.</span></span>
  
    
    
<span data-ttu-id="eb423-p120">Nach der Konvertierung werden Ihre HTML-Datei und die SharePoint-Gestaltungsvorlage verknüpft, sodass die Gestaltungsvorlage automatisch aktualisiert wird, wenn Sie die HTML-Datei bearbeiten und auf Ihrem zugeordneten Laufwerk speichern. Die HTML-Gestaltungsvorlage besitzt im Entwurfs-Manager eine Eigenschaft mit der Bezeichnung **Zugeordnete Datei**. Mit dieser Eigenschaft wird festgelegt, ob Änderungen an der HTML-Datei mit der .master-Datei synchronisiert werden.</span><span class="sxs-lookup"><span data-stu-id="eb423-p120">After the conversion, your HTML file and the SharePoint master page are associated, so that when you edit and save the HTML file in your mapped drive, the master page is updated automatically. In Design Manager, the HTML master page has a property named **Associated File** that determines whether changes to the HTML file are synced to the .master file.</span></span>
  
    
    

> <span data-ttu-id="eb423-179">**Hinweis:** Der Entwurfs-Manager bietet auch die Möglichkeit, eine minimale Gestaltungsvorlage als Grundlage für Ihr Design zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="eb423-179">**Note:** Design Manager also provides an option to begin your design by using a minimal master page.</span></span> <span data-ttu-id="eb423-180">In diesem Szenario müssen Sie nicht mit einem HTML-Design beginnen; Sie können stattdessen eine HTML-Gestaltungsvorlage mit allen Seitenelementen erstellen, die mindestens erforderlich sind, um die Gestaltungsvorlage korrekt in SharePoint zu rendern. Anschließend können Sie diese HTML-Gestaltungsvorlage bearbeiten, um Ihr Design anzupassen.</span><span class="sxs-lookup"><span data-stu-id="eb423-180">Design Manager also provides an option to begin your design by using a minimal master page. In this scenario, you don't have to begin with an HTML design; instead, you can create an HTML master page that contains the minimum page elements necessary to render the master page correctly in SharePoint, and then build out your design by editing the HTML master page.</span></span> 
  
    
    


#### <a name="preview-the-master-page"></a><span data-ttu-id="eb423-181">Anzeigen einer Vorschau der Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="eb423-181">Preview the master page</span></span>

<span data-ttu-id="eb423-p122">Zusätzlich zur Konvertierung Ihrer Gestaltungsvorlage bietet der Entwurfs-Manager eine serverseitige Vorschau (im Gegensatz zur Entwurfszeitvorschau in Ihrem HTML-Editor), sodass Sie eine Live-Vorschau Ihrer Gestaltungsvorlage erhalten und etwaige Probleme beheben können, die das Rendern der Seite verhindern können. Da Ihre HTML-Datei z. B. XML-konform sein muss, müssen Sie möglicherweise kleinere Markup-Probleme beheben und z. B. für alle Elemente schließende Tags angeben. Um Probleme zu beheben, sollten Sie die HTML-Datei bearbeiten, speichern und dann die serverseitige Vorschau aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="eb423-p122">In addition to converting your master page, Design Manager provides a server-side preview (vs. the design-time preview in your HTML editor), so that you can get a live preview of your master page and fix any issues that might prevent the page from rendering. For example, your HTML file must be XML-compliant, so you may have to fix minor markup issues such as providing closing tags for all elements. To fix any issues, you should edit the HTML file, save it, and then refresh the server-side preview.</span></span>
  
    
    
<span data-ttu-id="eb423-p123">Wenn Sie eine Gestaltungsvorlage in der Vorschau anzeigen, können Sie die Option **Vorschau-Seite ändern** links oben verwenden, um die Gestaltungsvorlage sowie jede vorhandene Seite in der Vorschau anzuzeigen, oder eine neue Seite erstellen, die in der Vorschau angezeigt werden soll. Im Gegensatz zur Entwurfszeitvorschau Ihrer HTML-Gestaltungsvorlage in einem HTML-Editor ist diese serverseitige Vorschau eine Live-Vorschau mit sämtlichen Funktionen. Daher ziehen Sie es möglicherweise vor, die HTML-Datei zu bearbeiten und speichern, sodass die verknüpfte .master-Datei mit den aktuellen Änderungen synchronisiert wird, die Live-Vorschau zu aktualisieren und die aktuellen Designänderungen im Browser anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="eb423-p123">When you preview a master page, you can use the **Change Preview Page** option in the top-left corner to preview the master page along with any existing page, or create a new page to preview with. Unlike the design-time preview of your HTML master page in an HTML editor, this server-side preview is a fully functional live preview, so you may prefer to edit the HTML file, save it so that the latest changes are synced to the associated .master file, and refresh the live preview and view your latest design changes in the browser.</span></span>
  
    
    

#### <a name="add-snippets"></a><span data-ttu-id="eb423-187">Hinzufügen von Ausschnitten</span><span class="sxs-lookup"><span data-stu-id="eb423-187">Add snippets</span></span>

<span data-ttu-id="eb423-p124">Nachdem Sie Ihre Gestaltungsvorlage konvertiert und erfolgreich in der Vorschau angezeigt haben, können Sie der Gestaltungsvorlage Ausschnitte hinzufügen. Ein Ausschnitt ist eine HTML-Darstellung einer SharePoint-Komponente, wie ein Navigationssteuerelement, ein Suchfeld oder ein Webpart, das Sie Ihrer Gestaltungsvorlage hinzufügen können. Durch Hinzufügen von Ausschnitten zu Ihrer Gestaltungsvorlage können Sie schnell eine breite Palette von SharePoint-Funktionen in Ihre Gestaltungsvorlage integrieren. Das Hinzufügen von Ausschnitten umfasst im Wesentlichen drei Schritte:</span><span class="sxs-lookup"><span data-stu-id="eb423-p124">After you convert your master page and successfully preview it, you are ready to add snippets to the master page. A snippet is an HTML representation of a SharePoint component—such as a navigation control or search box or Web Part—that you can add to your master page. Adding snippets to your master page is how you quickly build the full range of SharePoint functionality into your master page. Adding snippets is basically a three-step process:</span></span>
  
    
    

1. <span data-ttu-id="eb423-192">Suchen und Konfigurieren von Ausschnitten im Codeausschnittkatalog</span><span class="sxs-lookup"><span data-stu-id="eb423-192">Find and configure snippets in the Snippet Gallery.</span></span>
    
  
2. <span data-ttu-id="eb423-193">Kopieren von Ausschnitten in Ihre HTML-Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="eb423-193">Copy snippets to your HTML master page.</span></span>
    
  
3. <span data-ttu-id="eb423-194">Anzeigen von Ausschnitten in der Vorschau und Formatieren von Ausschnitten mit CSS</span><span class="sxs-lookup"><span data-stu-id="eb423-194">Preview and style snippets by using CSS.</span></span>
    
<span data-ttu-id="eb423-195">Weitere Informationen finden Sie unter  [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="eb423-195">For more information, see  [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
    
  

#### <a name="find-and-configure-snippets-in-the-snippet-gallery"></a><span data-ttu-id="eb423-196">Suchen und Konfigurieren von Ausschnitten im Codeausschnittkatalog</span><span class="sxs-lookup"><span data-stu-id="eb423-196">Find and configure snippets in the Snippet Gallery</span></span>

<span data-ttu-id="eb423-p125">Im Codeausschnittkatalog können Sie schnell sehen, welche Komponenten für den Typ von Datei verfügbar sind, die Sie bearbeiten: Gestaltungsvorlage oder Seitenlayout. Sie wählen auf dem Menüband einen Ausschnitt aus. Im Eigenschaftsraster auf der rechten Seite können Sie die Eigenschaften für diese Instanz eines Ausschnitts konfigurieren, und dann links **Aktualisieren** auswählen, um den HTML-Ausschnitt zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="eb423-p125">The Snippet Gallery is where you can quickly see which components are available for the type of file you're editing, either master page or page layout. On the ribbon, you select a snippet. In the property grid on the right, you can configure the properties for this instance of a snippet, and then choose **Update** to refresh the HTML snippet on the left.</span></span>
  
    
    

#### <a name="copy-snippets-to-your-html-master-page"></a><span data-ttu-id="eb423-200">Kopieren von Ausschnitten in Ihre HTML-Gestaltungsvorlage</span><span class="sxs-lookup"><span data-stu-id="eb423-200">Copy snippets to your HTML master page</span></span>

<span data-ttu-id="eb423-p126">Nachdem Sie einen Ausschnitt konfiguriert haben, kopieren Sie ihn in die Zwischenablage, und fügen Sie ihn dann in Ihrer HTML-Datei an der richtigen Stelle ein. Falls Ihr HTML-Design bereits Modellsteuerelemente oder statische Steuerelemente enthält, löschen oder kommentieren Sie diese aus, wenn Sie sie durch dynamische Ausschnitte aus der Codeausschnittkatalog ersetzen.</span><span class="sxs-lookup"><span data-stu-id="eb423-p126">After you configure a snippet, you copy it to the Clipboard and then paste it at the right spot in your HTML file. Your HTML design may already contain mockup or static controls, in which case you'll want to delete them or comment them out as you replace them with dynamic snippets from the Snippet Gallery.</span></span>
  
    
    

#### <a name="preview-and-style-snippets-by-using-css"></a><span data-ttu-id="eb423-203">Anzeigen von Ausschnitten in der Vorschau und Formatieren von Ausschnitten mit CSS</span><span class="sxs-lookup"><span data-stu-id="eb423-203">Preview and style snippets by using CSS</span></span>

<span data-ttu-id="eb423-p127">Nachdem Sie Ausschnitte in Ihre HTML-Datei kopiert und die Änderungen dann gespeichert haben, können Sie die serverseitige Vorschau der Gestaltungsvorlage aktualisieren, um zu sehen, wie das Steuerelement gerendert wird. Ausschnitte enthalten Markup, das eine Entwurfszeitvorschau in einem HTML-Editor ermöglicht. Die serverseitige Vorschau zeigt dagegen eine wirklich getreue Vorschau mit Livedaten an. So zeigt ein Navigationssteuerelement z. B. die aktuelle Navigationsstruktur der Website mit Livedaten aus Ihrer Datenquelle an.</span><span class="sxs-lookup"><span data-stu-id="eb423-p127">After you copy snippets into your HTML file and then save the changes, you can refresh the server-side preview of the master page to see how the control is rendered. Snippets contain markup that provides a design-time preview in an HTML editor, but the server-side preview shows a full-fidelity preview with live data—for example, a navigation control will show the site's current navigation structure with live data from your data source.</span></span>
  
    
    
<span data-ttu-id="eb423-p128">Die meisten Ausschnitte erben standardmäßig Formate vom SharePoint-Haupt-Stylesheet, corev15.css. Um einen Ausschnitt zu formatieren, müssen Sie ermitteln, welche Formate auf den Ausschnitt angewendet werden, und diese dann mit benutzerdefiniertem CSS überschreiben. Um diese Standardformate zu ermitteln, können Sie ein Browsertool wie die Entwicklertools in Internet Explorer verwenden. Drücken Sie, während Sie Ihre Gestaltungsvorlage in der serverseitigen Vorschau in Internet Explorer anzeigen, die Taste **F12**, wählen Sie **Suchen** und dann **Element durch Klicken auswählen** aus. Dann können Sie auf den Ausschnitt klicken und genau sehen, welche Formate überschrieben werden müssen, indem Sie dem entsprechenden benutzerdefinierten Stylesheet, mit dem Ihre Gestaltungsvorlage verknüpft ist, CSS hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="eb423-p128">By default, most snippets inherit styles from the main SharePoint style sheet, corev15.css. To style a snippet, you have to identify what styles are applied to the snippet and then override them with custom CSS. To identify these default styles, you can use a browser tool such as the developer tools in Internet Explorer. While viewing your master page in the server-side preview in Internet Explorer, press **F12**, choose **Find**, and then choose **Select element by click**. This lets you click the snippet and see exactly what styles to override by adding CSS to whatever custom style sheet your master page links to.</span></span>
  
    
    

### <a name="edit-display-templates"></a><span data-ttu-id="eb423-211">Bearbeiten von Anzeigevorlagen</span><span class="sxs-lookup"><span data-stu-id="eb423-211">Edit display templates</span></span>

<span data-ttu-id="eb423-p129">Wenn Sie eine lokale Installation von SharePoint Server verwenden, können Sie mit dem Inhaltssuche-Webpart und anderen suchbasierten Webparts die Ergebnisse Ihrer Suchabfragen als Inhalte in Ihren Seiten anzeigen. Suchbasierte Webparts zeigen Vorlagen im Wesentlichen zu zwei Zwecken an:</span><span class="sxs-lookup"><span data-stu-id="eb423-p129">If you are using an on-premises installation of SharePoint Server, you can use the Content Search Web Part and other search-driven Web Parts to display the results of search queries as content on your pages. Search-driven Web Parts use display templates for two main purposes:</span></span>
  
    
    

- <span data-ttu-id="eb423-214">Um die verwalteten Eigenschaften, die in Suchergebniselementen zurückgegeben werden, Eigenschaften zuzuordnen, die für JavaScript verfügbar sind, einschließlich des benutzerdefinierten JavaScript, das Sie implementieren möchten.</span><span class="sxs-lookup"><span data-stu-id="eb423-214">To map the managed properties that are returned in search-result items to properties that will be available for JavaScript, including whatever custom JavaScript you choose to implement.</span></span>
    
  
- <span data-ttu-id="eb423-215">Um diese Eigenschaften mithilfe von HTML und CSS anzuzeigen und die Anzeige zu formatieren.</span><span class="sxs-lookup"><span data-stu-id="eb423-215">To use HTML and CSS to present and style how those properties are displayed.</span></span>
    
  
<span data-ttu-id="eb423-p130">Bei Gestaltungsvorlagen und Seitenlayouts bearbeiten Sie eine verknüpfte HTML-Datei, jedoch nicht die .master-Datei oder die .aspx-Datei. Auf ähnliche Weise bestehen Anzeigevorlagen aus einer HTML-Datei und einer verknüpften .js-Datei, wobei Sie nur die HTML-Datei bearbeiten. Jedes Mal, wenn Sie die HTML-Datei speichern, aktualisiert SharePoint automatisch die verknüpfte .js-Datei.</span><span class="sxs-lookup"><span data-stu-id="eb423-p130">With master pages and page layouts, you edit an associated HTML file but not the .master file or .aspx file. Similarly, display templates are made of an HTML file and an associated .js file, where you edit only the HTML file. Each time you save that HTML file, SharePoint automatically updates the associated .js file.</span></span>
  
    
    
<span data-ttu-id="eb423-p131">Wenn Sie eine benutzerdefinierte Anzeigevorlage erstellen möchten, sollten Sie zunächst eine der vorhandenen Anzeigevorlagen kopieren und dann bearbeiten. Dies ist hilfreich, da die Standardanzeigevorlagen in Kommentaren in den HTML-Dateien Informationen enthalten und Sie die richtige Seitengrundstruktur und einen Rahmen für einfache Aufgaben wie das Zuordnen von Eingabefeldern zur Hand haben.</span><span class="sxs-lookup"><span data-stu-id="eb423-p131">When you want to create a custom display template, you should begin by copying and then modifying one of the existing display templates. This is helpful because the default display templates contain information in comments in the HTML files, and you'll have the proper basic page structure and a framework in place for basic tasks like mapping input fields.</span></span>
  
    
    

### <a name="edit-page-layouts"></a><span data-ttu-id="eb423-221">Bearbeiten von Seitenlayouts</span><span class="sxs-lookup"><span data-stu-id="eb423-221">Edit page layouts</span></span>

<span data-ttu-id="eb423-p132">Der Prozess zur Erstellung eines Seitenlayouts unterscheidet sich ein wenig vom Prozess zur Erstellung einer Gestaltungsvorlage. Bei einer Gestaltungsvorlage beginnen Sie mit einem HTML-Design, konvertieren dieses in eine SharePoint-Gestaltungsvorlage und bearbeiten dann weiterhin die verknüpfte HTML-Datei. Bei einem Seitenlayout hingegen erstellen Sie zuerst das Seitenlayout im Entwurfs-Manager, der eine .aspx-Datei und eine HTML-Datei erstellt, und bearbeiten dann in Ihrem HTML-Editor die verknüpfte HTML-Datei auf dem zugeordneten Laufwerk. Der Grund dafür, dass Sie den Entwurfs-Manager zum Erstellung eines Seitenlayouts verwenden müssen, ist, dass dem Seitenlayout der korrekte Satz von Seitenfeldern hinzugefügt werden kann.</span><span class="sxs-lookup"><span data-stu-id="eb423-p132">The process for creating a page layout is a bit different from that for creating a master page. For a master page, you start with an HTML design, convert that into a SharePoint master page, and then continue to edit the associated HTML file. But for a page layout, you first create the page layout in Design Manager, which creates an .aspx file and an HTML file, and then you edit the associated HTML file from the mapped drive in your HTML editor. The reason you have to use Design Manager to create a page layout is so that the correct set of page fields can get added to the page layout.</span></span>
  
    
    
<span data-ttu-id="eb423-p133">Wenn Sie ein Seitenlayout erstellen, wählen Sie eine Gestaltungsvorlage, mit der Sie Ihr Seitenlayout in der Vorschau anzeigen, sowie einen Seitenlayout-Inhaltstypen aus. Ein Inhaltstyp ist ein Schema von Feldern und Datentypen, und die im Seitenlayout-Inhaltstyp verfügbaren Felder bestimmen, welche Seitenfeld-Steuerelemente im von Ihnen entworfenen Seitenlayout verfügbar sind. Sie erstellen zuerst ein Seitenlayout im Browser, sodass die Seitenfelder hinzugefügt werden können.</span><span class="sxs-lookup"><span data-stu-id="eb423-p133">When you create a page layout, you select a master page with which to preview your page layout, and you select a Page Layout Content Type. A content type is a schema of fields and data types, and the fields available in the page layout content type determine what page field controls are available on the page layout that you design. You create a page layout in the browser first so that the page fields can be added.</span></span>
  
    
    
<span data-ttu-id="eb423-229">Nachdem Sie ein Seitenlayout mit der verknüpften HTML-Datei erstellt haben, sind die restlichen Schritte die gleichen wie bei einer Gestaltungsvorlage:</span><span class="sxs-lookup"><span data-stu-id="eb423-229">After you create a page layout with its associated HTML file, the remaining steps are the same as for a master page:</span></span>
  
    
    

- <span data-ttu-id="eb423-230">Anzeigen des Seitenlayouts in der Vorschau und Beheben etwaiger Probleme durch das Bearbeiten und Speichern der HTML-Version</span><span class="sxs-lookup"><span data-stu-id="eb423-230">Preview the page layout and fix any issues by editing and saving the HTML version.</span></span>
    
  
- <span data-ttu-id="eb423-231">Hinzufügen von Ausschnitten zum Seitenlayout (Konfigurieren, Kopieren, in der Vorschau anzeigen, Formatieren)</span><span class="sxs-lookup"><span data-stu-id="eb423-231">Add snippets to the page layout (configure, copy, preview, style).</span></span>
    
  
<span data-ttu-id="eb423-p134">In der Codeausschnittgalerie sind für Seitenlayouts und Gestaltungsvorlagen verschiedene Ausschnitte verfügbar, und das Menüband zeigt nur die Ausschnitte an, die für diesen Dateityp relevant sind. So sind z. B. Navigations- und Suchfeldausschnitte nur für eine Gestaltungsvorlage verfügbar, während Seitenfelder nur in einem Seitenlayout verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="eb423-p134">In the Snippet Gallery, different snippets are available for page layouts and master pages, and the ribbon displays only the snippets that are relevant for that type of file. For example, navigation and search box snippets are available only for a master page, while page fields are available only on a page layout.</span></span>
  
    
    
<span data-ttu-id="eb423-p135">Wenn Sie ein Seitenlayout entwerfen, besteht Ihre wichtigste Aufgabe darin, die Seitenfeldsteuerelemente zu positionieren und zu formatieren, die von Inhaltsautoren erstellte Inhalte anzeigen. Die Formate für ein Seitenlayout können sich in einem Stylesheet befinden, mit dem die Gestaltungsvorlage verknüpft ist, oder jedes Seitenlayout kann mit einem eigenen spezifischen Stylesheet verknüpft sein. Wenn Ihr HTML-Design geeignetere Inhalte für ein Seitenlayout enthält als eine Gestaltungsvorlage, sollten Sie diese Inhalte aus Ihrer HTML-Gestaltungsvorlage übertragen und diese Formate dann auf die richtigen Steuerelemente und Elemente des relevanten Seitenlayouts anwenden.</span><span class="sxs-lookup"><span data-stu-id="eb423-p135">When you design a page layout, your basic task is to position and style the page field controls that will display content created by content authors. The styles for a page layout can reside in whatever style sheet the master page links to, or each page layout can link to its own specific style sheet. If your HTML design includes content more suitable for a page layout than a master page, you want to transfer that content out of your HTML master page, and then apply those styles to the correct controls and elements of the relevant page layout.</span></span>
  
    
    
<span data-ttu-id="eb423-237">Weitere Informationen finden Sie unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="eb423-237">For more information, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
  
    
    

### <a name="create-themes-and-composed-looks"></a><span data-ttu-id="eb423-238">Erstellen von Design und zusammengesetzten Layouts</span><span class="sxs-lookup"><span data-stu-id="eb423-238">Create themes and composed looks</span></span>

<span data-ttu-id="eb423-239">In Office 365 können Sie mit dem Entwurfs-Manager Designs und durchkomponierte Looks erstellen. (Diese Möglichkeit besteht nicht in lokalen SharePoint-Installationen.)</span><span class="sxs-lookup"><span data-stu-id="eb423-239">In the Office 365, but not in on-premises SharePoint installations, Design Manager has the option of creating themes and composed looks.</span></span> <span data-ttu-id="eb423-240">Ein Design ist ein Satz von Schriftarten und Farben, das auf ein benutzerdefiniertes Design angewendet werden kann (d. h. eine Gestaltungsvorlage).</span><span class="sxs-lookup"><span data-stu-id="eb423-240">A theme is a set of fonts and colors that can be applied to a custom design (meaning a master page).</span></span> <span data-ttu-id="eb423-241">Designs werden in XML-Dateien definiert, die wiederum in den Designkatalog hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="eb423-241">Themes are defined in .xml files that you upload to the Themes gallery.</span></span> <span data-ttu-id="eb423-242">Soll eine benutzerdefinierte Gestaltungsvorlage Designs unterstützen, müssen Sie der Gestaltungsvorlage spezielles Markup hinzufügen. SharePoint erkennt dieses Markup und fügt Designelemente wie Schriftarten und Farben ein.</span><span class="sxs-lookup"><span data-stu-id="eb423-242">If you want a custom master page to be theme-able, you need to add special markup to the master page that SharePoint recognizes and uses to insert theme elements such as fonts and colors.</span></span>
  
    
<span data-ttu-id="eb423-243">Ein durchkomponierter Look besteht aus einem Hintergrundbild, einem Design (d. h. Schriftarten und Farben) und einer Gestaltungsvorlage.</span><span class="sxs-lookup"><span data-stu-id="eb423-243">A composed look is just an association between a background image, a theme (meaning fonts and colors), and a design (meaning a master page). A composed look takes predefined design elements—themes, background images, and master pages—and enables them to be used in many different combinations, so that the public-facing website has many more customization options.</span></span> <span data-ttu-id="eb423-244">Mithilfe eines durchkomponierten Looks können Sie vordefinierte Designelemente (Designs, Hintergrundbilder und Gestaltungsvorlagen) in den unterschiedlichsten Kombinationen verwenden.</span><span class="sxs-lookup"><span data-stu-id="eb423-244">A composed look takes predefined design elements—themes, background images, and master pages—and enables them to be used in many different combinations.</span></span>
  
    

### <a name="publish-and-apply-design"></a><span data-ttu-id="eb423-245">Veröffentlichen und Anwenden eines Designs</span><span class="sxs-lookup"><span data-stu-id="eb423-245">Publish and apply design</span></span>

<span data-ttu-id="eb423-p138">Die meisten von Ihrem Design verwendeten Objekte, wie Bilder, HTML-, CSS- und JavaScript-Dateien, befinden sich in der Gestaltungsvorlagengalerie. Die Gestaltungsvorlagengalerie ist eine SharePoint-Dokumentbibliothek mit standardmäßig aktivierter Versionsverwaltung, sodass jedes Mal, wenn Sie eine Datei bearbeiten, Haupt- und Nebenversionen (Entwurfsversionen) erstellt werden.</span><span class="sxs-lookup"><span data-stu-id="eb423-p138">Most assets used by your design, such as images, HTML, CSS, and JavaScript files, will reside in the Master Page Gallery. The Master Page Gallery is a SharePoint document library that by default has versioning turned on, which creates major and minor (draft) versions each time you edit a file.</span></span>
  
    
    
<span data-ttu-id="eb423-p139">Bevor Sie Ihr Design auf eine Website anwenden können, müssen Sie zuerst eine Hauptversion jeder Datei oder jedes Objekts veröffentlichen, das von Ihrem Design verwendet wird. Wenn Sie Ihre Website in einer Testumgebung entwerfen, sollten Sie die Versionsverwaltung für die Gestaltungsvorlagengalerie deaktivieren, sodass Sie nicht jede Datei veröffentlichen müssen, bevor Sie die Website in der Vorschau anzeigen. Dies wird jedoch nicht empfohlen, wenn Sie Ihr Design auf einer Livewebsite entwerfen.</span><span class="sxs-lookup"><span data-stu-id="eb423-p139">Before you can apply your design to a site, you first have to publish a major version of each file or asset used by your design. If you are designing your site in a test environment, you should turn off versioning for the Master Page Gallery, so that you don't have to remember to publish every file before you preview the site. But this is not a best practice if you are designing on a live site.</span></span>
  
    
    
<span data-ttu-id="eb423-p140">Wenn Sie alle Designdateien veröffentlicht haben, können Sie das Design anwenden, indem Sie Ihrer Website Ihre fertigen Gestaltungsvorlagen zuweisen. Jede Website kann jedem Gerätekanal eine andere Gestaltungsvorlage zuweisen, und auf dieser Seite des Entwurfs-Managers wenden Sie eine Gestaltungsvorlage auf einen Kanal an.</span><span class="sxs-lookup"><span data-stu-id="eb423-p140">After you publish all the design files, you are ready to apply the design by assigning your finished master pages to your site. Each site can have a different master page assigned to each device channel, and this page of Design Manager is where you apply a master page to a channel.</span></span>
  
    
    

### <a name="create-a-design-package"></a><span data-ttu-id="eb423-253">Erstellen eines Designpakets</span><span class="sxs-lookup"><span data-stu-id="eb423-253">Create a design package</span></span>

<span data-ttu-id="eb423-p141">Ein Designpaket stellt eine einfache Möglichkeit dar, alle von Ihrem Design verwendeten Dateien und Objekte zu sammeln, sie von einer Website zu exportieren, sie in eine andere Website zu importieren und das Design auf die neue Website anzuwenden. Wenn Sie Ihr Design in einer Testwebsitesammlung implementieren und optimieren und es in einer Livewebsitesammlung bereitstellen möchten, können Sie zum Übertragen Ihres Designs ein Designpaket verwenden.</span><span class="sxs-lookup"><span data-stu-id="eb423-p141">A design package is an easy way to collect all the files and assets used by your design, export them from one site, import them into another site, and apply the design to the new site. If you implement and polish your design in a test site collection and want to deploy it in a live site collection, you can use a design package to transfer your design.</span></span>
  
    
    
<span data-ttu-id="eb423-p142">Ein Designpaket ist eine .wsp-Datei, eine SharePoint-Lösungsdatei, bei der es sich im Grunde um einen speziellen Typ von .cab-Datei handelt. Wenn Sie ein Designpaket erstellen oder importieren, wird die .wsp-Datei in der Lösungsgalerie gespeichert. Nachdem Sie ein Designpaket importiert haben, wird das Paket automatisch aktiviert. Wenn die Gestaltungsvorlagen und Seitenlayouts veröffentlicht wurden, bevor sie verpackt wurden, und wenn die Gestaltungsvorlagen Gerätekanälen zugeordnet wurden, bevor sie verpackt wurden, wird das Design automatisch auf die Website angewendet, wenn das Designpaket bereitgestellt wird. Um das Design auf die neue Website anzuwenden, müssen Sie ansonsten einfach die Designdateien veröffentlichen und die Gestaltungsvorlagen pro Gerätekanal anwenden.</span><span class="sxs-lookup"><span data-stu-id="eb423-p142">A design package is a .wsp file, a SharePoint solution file, which is basically a special type of .cab file. When you create or import a design package, the .wsp file is stored in the Solutions gallery. After you import a design package, the package is automatically activated. If the master pages and page layouts were published before they were packaged, and if the master pages were assigned to device channels before they were packaged, the design will be automatically applied to the site when the design package is deployed. Otherwise, to apply the design to the new site, you just have to publish the design files and apply the master pages per device channel.</span></span>
  



## <a name="additional-resources"></a><span data-ttu-id="eb423-261">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="eb423-261">Additional resources</span></span>
<span data-ttu-id="eb423-262"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="eb423-262"></span></span>


-  [<span data-ttu-id="eb423-263">Übersicht über das SharePoint-Seitenmodell</span><span class="sxs-lookup"><span data-stu-id="eb423-263">Overview of the SharePoint page model</span></span>](overview-of-the-sharepoint-page-model.md)
    
  
-  [<span data-ttu-id="eb423-264">Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint</span><span class="sxs-lookup"><span data-stu-id="eb423-264">How to: Convert an HTML file into a master page in SharePoint</span></span>](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="eb423-265">Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="eb423-265">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  

