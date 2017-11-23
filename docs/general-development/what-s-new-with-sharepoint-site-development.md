---
title: Neuigkeiten in der SharePoint-Websiteentwicklung
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: ac1e9891-5ce9-4707-84e5-6e2fc02fda6b
ms.openlocfilehash: aa697345fd77c86159a94de4f5c91b79ead99e73
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="whats-new-with-sharepoint-site-development"></a><span data-ttu-id="c080a-102">Neuigkeiten in der SharePoint-Websiteentwicklung</span><span class="sxs-lookup"><span data-stu-id="c080a-102">What's new with SharePoint site development</span></span>
<span data-ttu-id="c080a-103">Informationen über das neue Erstellungs -und Veröffentlichungsmodell in SharePoint zur Veröffentlichung von Websites.</span><span class="sxs-lookup"><span data-stu-id="c080a-103">Learn about the new site authoring and publishing model in SharePoint that enables you to create publishing sites.</span></span>
## <a name="introduction-to-site-publishing-for-designers-and-developers-in-sharepoint"></a><span data-ttu-id="c080a-104">Einführung in die Websiteveröffentlichung für Designer und Entwickler in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c080a-104">Introduction to site publishing for designers and developers in SharePoint</span></span>
<span data-ttu-id="c080a-105"><a name="SP15_WhatsNewSiteDevelopment_IntroductionToSitePublishing"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-105"></span></span>

<span data-ttu-id="c080a-106">SharePoint führt die folgenden Features neu ein. Sie unterstützen den Workflow einer ECM-Websiteerstellung (Enterprise Content Management) für Veröffentlichungssites.</span><span class="sxs-lookup"><span data-stu-id="c080a-106">The following features are new in SharePoint and support the enterprise content management (ECM) site creation workflow for publishing sites.</span></span>
  
    
    

### <a name="client-programming-models-for-publishing-site-development"></a><span data-ttu-id="c080a-107">Clientprogrammierungsmodelle für die Entwicklung von Veröffentlichungssites</span><span class="sxs-lookup"><span data-stu-id="c080a-107">Client programming models for publishing site development</span></span>

<span data-ttu-id="c080a-p101">In SharePoint können Sie das .NET-Clientobjektmodell (CSOM), Silverlight und die JavaScript-Programmierungsmodelle zum Entwickeln von benutzerdefinierten Websites, Sitekomponenten, Branding-Elementen und Verhalten verwenden. Viele der für die .NET-Serverprogrammierung verfügbaren APIs finden Sie im entsprechenden .NET-Client (CSOM), in Silverlight und in JavaScript-Assemblys. In einigen Fällen sind die entsprechenden APIs auch in Windows Phone-Bibliotheken verfügbar.</span><span class="sxs-lookup"><span data-stu-id="c080a-p101">In SharePoint, you can use the .NET client object model (CSOM), Silverlight, and JavaScript programming models to develop custom sites, site components, branding elements, and behavior. Most APIs available for .NET server programming are available in corresponding .NET client (CSOM), Silverlight, and JavaScript assemblies. In some cases, corresponding APIs are also available in Windows Phone libraries.</span></span>
  
    
    
<span data-ttu-id="c080a-p102">Weitere Informationen finden Sie in den Referenzhomepages zu Websites und Inhalten für  [.NET-Server](http://msdn.microsoft.com/library/8a93e838-234c-41d8-b990-7ac1a415dd5e%28Office.15%29.aspx),  [.NET-Client](http://msdn.microsoft.com/library/e6542022-a459-4c3b-aee0-e350c6397139%28Office.15%29.aspx) und [JavaScript](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx). Sie können auch mit der  [-Referenzhomepage](http://msdn.microsoft.com/library/7940ba4e-f6f0-4bc0-b995-ceb2d358ca0d%28Office.15%29.aspx) beginnen, falls Sie ganz oben beginnen möchten und dann die Inhalte der einzelnen Programmierungsmodelle kennen lernen wollen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p102">To learn more, see the reference home pages for sites and content for  [.NET server](http://msdn.microsoft.com/library/8a93e838-234c-41d8-b990-7ac1a415dd5e%28Office.15%29.aspx),  [.NET client](http://msdn.microsoft.com/library/e6542022-a459-4c3b-aee0-e350c6397139%28Office.15%29.aspx), and  [JavaScript](http://msdn.microsoft.com/library/1ead2f8d-a541-4a50-89fa-f195f2ba14e5%28Office.15%29.aspx). Or, start with the  [reference home page](http://msdn.microsoft.com/library/7940ba4e-f6f0-4bc0-b995-ceb2d358ca0d%28Office.15%29.aspx) if you want to start at the top and then explore the contents of each programming model.</span></span>
  
    
    

### <a name="using-publishing-and-taxonomy-apis-with-the-new-sharepoint-app-model"></a><span data-ttu-id="c080a-113">Verwenden von Veröffentlichungs- und Taxonomie-APIs im neuen SharePoint-App-Modell</span><span class="sxs-lookup"><span data-stu-id="c080a-113">Using publishing and taxonomy APIs with the new SharePoint app model</span></span>

<span data-ttu-id="c080a-114">Sie können benutzerdefinierten Client- und Servercode in SharePoint-Add-Ins schreiben und damit die SharePoint-Veröffentlichungs- und Taxonomiefunktionalität erweiterten. Diese steht den Benutzern auf der Benutzeroberfläche (UI) bereit.</span><span class="sxs-lookup"><span data-stu-id="c080a-114">You can write custom client and server code in SharePoint Add-ins that extend the SharePoint publishing and taxonomy functionality that's available to users through the user interface (UI).</span></span> 
  
    
    
<span data-ttu-id="c080a-115">Einige Punkte bei der Entwicklung von Apps, die eine Websiteveröffentlichung verbessern, sind Umfragen, Kontoverwaltungs-Apps, eCommerce-Support, Apps, die soziale Funktionen und externe Daten in Veröffentlichungssites beinhalten, ausgelagerte zusätzliche Inhalte sowie mobile Begleit-Apps.</span><span class="sxs-lookup"><span data-stu-id="c080a-115">Some ideas for developing apps that enhance site publishing include surveys, account management apps, eCommerce support, apps that integrate social features and external data into publishing sites, outsourced content additions to your sites, and mobile companion apps.</span></span>
  
    
    

## <a name="authoring-design-and-branding-features"></a><span data-ttu-id="c080a-116">Erstellungs-, Entwurfs- und Branding-Features</span><span class="sxs-lookup"><span data-stu-id="c080a-116">Authoring, design, and branding features</span></span>
<span data-ttu-id="c080a-117"><a name="SP15_WhatsNewSiteDevelopment_AuthoringAndBranding"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-117"></span></span>

<span data-ttu-id="c080a-118">SharePoint enthält Features und APIs für das Erstellen, Entwerfen, Branding und Erweitern Ihrer Website, des Websitedesigns, der Branding-Elemente und des Websiteverhaltens.</span><span class="sxs-lookup"><span data-stu-id="c080a-118">SharePoint includes features and APIs that you can use to author, design, brand, and extend your site, site design and branding elements, and behaviors.</span></span> 
  
    
    

### <a name="design-manager"></a><span data-ttu-id="c080a-119">Design Manager</span><span class="sxs-lookup"><span data-stu-id="c080a-119">Design Manager</span></span>

<span data-ttu-id="c080a-p103">In früheren SharePoint-Versionen benötigte das Branding einer Website spezielle technische Kenntnisse beispielsweise zu Inhaltsplatzhaltern auf der Masterseite oder wie eine Masterseite bestimmte Steuerelementformatklassen bereitstellt. SharePoint führt den  [Entwurfs-Manager](overview-of-design-manager-in-sharepoint.md) ein, die neue Schnittstelle und zentraler Hub für die Verwaltung aller Branding-Aspekte auf Ihrer SharePoint-Website. Sie finden den Entwurfs-Manager auf der obersten Website Ihrer Websitesammlung. Er ist Teil der Websitesammlungsvorlage "Veröffentlichungsportal" in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c080a-p103">In previous versions of SharePoint, branding a site required specific technical expertise about things like what content placeholders are required on a master page, or how a master page implements certain classes of styles. SharePoint introduces  [Design Manager](overview-of-design-manager-in-sharepoint.md)—a new interface and central hub for managing all aspects of branding your SharePoint site. You can find the Design Manager in the top-level site for your site collection. It is a part of the Publishing Portal site collection template in SharePoint.</span></span>
  
    
    
<span data-ttu-id="c080a-124">Der Entwurfs-Manager ermöglicht eine schrittweise Herangehensweise für das Erstellen von Designobjekten, die Sie für das Branding von Websites verwenden können.</span><span class="sxs-lookup"><span data-stu-id="c080a-124">Design Manager enables a step-by-step approach for creating design assets that you can use to brand sites.</span></span> <span data-ttu-id="c080a-125">Laden Sie zunächst die Designobjekte (Bilder, HTML, CSS usw.) hoch, und erstellen Sie dann Ihre Gestaltungsvorlagen und Seitenlayouts.</span><span class="sxs-lookup"><span data-stu-id="c080a-125">Upload design assets—images, HTML, CSS, and so on—and then create your master pages and page layouts.</span></span> <span data-ttu-id="c080a-126">Während des Entwurfs können Sie in einer Vorschau anzeigen, wie das Design in einem clientseitigen Codeeditor oder auf dem Server aussieht.</span><span class="sxs-lookup"><span data-stu-id="c080a-126">You can preview how your design looks either in a client-side code editor or on the server as you are designing it.</span></span> <span data-ttu-id="c080a-127">Sie können benutzerdefinierte SharePoint-Komponenten und Menübandelemente mithilfe der Entwurfs-Manager-Benutzeroberfläche hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c080a-127">You can add custom SharePoint components and ribbon elements by using the Design Manager UI.</span></span> <span data-ttu-id="c080a-128">Der Entwurfs-Manager generiert HTML-[Codeausschnitte](sharepoint-design-manager-snippets.md), die mit jedem Webdesigntool verwendet werden können. Er rendert HTML- und ignoriert ASP.NET- und SharePoint-Markup (während SharePoint nur ASP.NET- und SharePoint-Markup rendert und HTML.md ignoriert).</span><span class="sxs-lookup"><span data-stu-id="c080a-128">Design Manager generates HTML snippets that can be used by any web design tool—it just renders HTML and ignores ASP.NET and SharePoint markup. SharePoint renders only ASP.NET and SharePoint markup and ignores HTML.</span></span>
  
    
    
<span data-ttu-id="c080a-129">Sie können Ihre Kenntnisse in HTML, CSS und JavaScript zum Entwerfen von Gestaltungsvorlagen in HTML nutzen und HTML-Seitenlayouts im HTML-Editor Ihrer Wahl entwerfen.</span><span class="sxs-lookup"><span data-stu-id="c080a-129">You can use your expertise in HTML, CSS, and JavaScript to design master pages in HTML, and design HTML page layouts in the HTML editor of your choice.</span></span> <span data-ttu-id="c080a-130">Um Ihr bevorzugtes Erstellungs- und Designtool mit Ihrer SharePoint-Website zu verbinden, [ordnen Sie ein Netzlaufwerk zu](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md), und bearbeiten Sie dann die SharePoint-Datei, als wäre sie eine lokale Datei.</span><span class="sxs-lookup"><span data-stu-id="c080a-130">To connect your favorite authoring and design tool to your SharePoint site,  [map a network drive](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md) and then edit the SharePoint file as if it were a local file.</span></span> <span data-ttu-id="c080a-131">Wenn Ihr Websitedesign fertig ist, laden Sie den HTML-Code und die unterstützenden Dateien hoch, und verwenden Sie den Entwurfs-Manager, um die [HTML-Datei in eine ASP.NET-Gestaltungsvorlage (.master.md-Datei) zu konvertieren](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c080a-131">When your site design is ready, upload the HTML and supporting files and use Design Manager to [convert the HTML file into an ASP.NET master page (.master.md) file](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md).</span></span> <span data-ttu-id="c080a-132">Jetzt [wenden Sie die Gestaltungsvorlage](how-to-apply-a-master-page-to-a-site-in-sharepoint.md) auf Ihre SharePoint-Website an.</span><span class="sxs-lookup"><span data-stu-id="c080a-132">Now,  [apply the master page](how-to-apply-a-master-page-to-a-site-in-sharepoint.md) to your SharePoint site.</span></span> <span data-ttu-id="c080a-133">Verwenden Sie den Entwurfs-Manager zum [Erstellen eines neuen Seitenlayouts](how-to-create-a-page-layout-in-sharepoint.md); die HTML-Version wird automatisch der entsprechenden ASP.NET-Seite (.aspx Datei.md) zugeordnet, die SharePoint interpretiert.</span><span class="sxs-lookup"><span data-stu-id="c080a-133">Use Design Manager to [create a new page layout](how-to-create-a-page-layout-in-sharepoint.md), and the HTML version of it is automatically associated with the corresponding ASP.NET page (.aspx file.md) that SharePoint interprets.</span></span> 
  
    
    
<span data-ttu-id="c080a-p106">Nachdem Sie Ihre HTML-Dateien konvertiert haben, verfeinern Sie Ihren Entwurf im HTML-Editor, zeigen Ihre Dateien in einer Vorschau an und speichern sie. Immer wenn Sie HTML-Versionen der Masterseite oder der Seitenlayoutdateien speichern, aktualisiert SharePoint automatisch die damit verbundene SharePoint-Masterseite und die Seitenlayouts, um den Änderungen Rechnung zu tragen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p106">After you convert your HTML files, you can use your HTML editor to continue to refine your design, preview your files, and save them. Every time you save the HTML versions of the master page or page layout files, SharePoint automatically updates the associated SharePoint master page and page layouts to reflect your changes.</span></span> 
  
    
    
<span data-ttu-id="c080a-136">Mit dem Entwurfs-Manager müssen Sie nur die HTML-Dateien bearbeiten. Sie können weiterhin benutzerdefinierte Masterseite und Seitenlayouts mit Ihren ASP.NET- und SharePoint-Entwicklungskenntnissen erstellen. Der Entwurfs-Manager befähigt Sie auch ohne große SharePoint-Entwicklerkenntnisse, großartige Websites zu entwerfen.</span><span class="sxs-lookup"><span data-stu-id="c080a-136">With Design Manager, you only have to edit the HTML files—while you can continue to write custom master pages and page layouts using your ASP.NET and SharePoint development skills, Design Manager enables you to design great sites without SharePoint developer expertise.</span></span>
  
    
    
<span data-ttu-id="c080a-p107">SharePoint beinhaltet auch HTML-Versionen mehrerer Masterseiten und Seitenlayouts, die Sie als Startvorlagen nutzen können. Wenn Sie mit diesen Dateien beginnen möchten, erstellen Sie eine Kopie der HTML-Seite (die verknüpfte ASP.NET-Datei wird automatisch verarbeitet), und bearbeiten Sie dann die HTML-Datei in der üblichen Weise. Sie können auch mit einer Basisvorlage beginnen, indem Sie die Option **Masterseite aus Minimalvorlage** verwenden, die dann selbsttätig die damit verbundene .master-Datei erstellt.</span><span class="sxs-lookup"><span data-stu-id="c080a-p107">If you prefer, SharePoint also includes HTML versions of several master pages and page layouts that you can use as starter templates. If you want to start from these files, create a copy of the HTML file (the associated ASP.NET file will be taken care of for you), and then edit the HTML file as you normally would. You can also start from just a basic template by using the **master page from minimal template** option, which automatically creates the associated .master file.</span></span>
  
    
    

### <a name="snippet-gallery"></a><span data-ttu-id="c080a-140">Codeausschnittkatalog</span><span class="sxs-lookup"><span data-stu-id="c080a-140">Snippet Gallery</span></span>

<span data-ttu-id="c080a-p108">SharePoint enthält viele einsatzbereite Komponenten, wie Webparts und Steuerelemente, die Sie Ihren Webseiten hinzufügen können. Beispiel: Sie fügen eine SharePoint-Komponente, wie ein Suchfeld oder ein Navigationssteuerelement, in die HTML-Masterseite ein, um somit schnell und einfach viel Funktionalität in Ihre Seiten einzubauen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p108">SharePoint contains many ready-to-use components—like Web Parts and controls—that you can add to your site's pages. For example, by inserting a SharePoint component such as a search box or navigation control into your HTML master page, you can quickly and easily build a lot of functionality into your pages.</span></span>
  
    
    
<span data-ttu-id="c080a-143">In der Gruppe **Codeausschnittkatalog** des Menübands können Sie eine Komponente auswählen, ihre Eigenschaften konfigurieren und den Codeausschnitt aktualisieren, den generierten HTML-Codeausschnitt kopieren und diesen HTML-Codeausschnitt in Ihre HTML-Datei einfügen.</span><span class="sxs-lookup"><span data-stu-id="c080a-143">On the ribbon, in the **Snippet Gallery** group, you can select a component, configure its properties and update the snippet, copy the HTML snippet that's generated, and paste that HTML snippet into your HTML file.</span></span> <span data-ttu-id="c080a-144">Der HTML-Codeausschnitt bietet Ihnen eine äußerste präzise Vorschau der Komponente, sowohl in der serverseitigen Vorschau als auch im HTML-Editor Ihrer Wahl.</span><span class="sxs-lookup"><span data-stu-id="c080a-144">The HTML snippet gives you a high-fidelity preview of that component, both in the server-side preview and in your HTML editor of choice.</span></span> <span data-ttu-id="c080a-145">Nachdem Sie Ihren HTML-Dateien SharePoint-Komponenten hinzugefügt haben, können Sie CSS für das vollständige Branding verwenden.</span><span class="sxs-lookup"><span data-stu-id="c080a-145">After you add SharePoint components to your HTML files, you can use CSS to fully brand them.</span></span> <span data-ttu-id="c080a-146">Ebenso wie bei jeder Aktualisierung der HTML-Datei werden die Änderungen nach dem Hinzufügen von SharePoint-Komponenten und ihrem Branding automatisch mit der zugeordneten Gestaltungsvorlage bzw. dem Seitenlayout synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="c080a-146">And just like any update to the HTML file, after you add SharePoint components and brand them, the changes are automatically synchronized to the associated master page or page layout.</span></span> <span data-ttu-id="c080a-147">Die HTML-Codeausschnitte werden automatisch in SharePoint-Komponenten konvertiert.</span><span class="sxs-lookup"><span data-stu-id="c080a-147">The HTML snippets are automatically converted into SharePoint components.</span></span>
  
    
    
 <span data-ttu-id="c080a-p110">Unabhängig davon, ob die HTML-Datei eine Masterseite oder ein Seitenlayout ist, zeigt der Codeausschnittkatalog die benötigten Komponenten an. Falls Sie nicht den benötigten Codeausschnitt entdecken, können Sie immer noch einen HTML-Codeausschnitt des ASP.NET-Markup erstellen und diesem zur HTML-Masterseite bzw. zum Seitenlayout hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p110">Whether your HTML file is a master page or a page layout, the Snippet Gallery shows you the components that you need. If you don't see the snippet you want, you can create an HTML snippet of ASP.NET markup and add that to your HTML master page or page layout.</span></span>
  
    
    
<span data-ttu-id="c080a-p111">Der Entwurfs-Manager generiert HTML-Codeausschnitte, die mit jedem Webentwurfstool verwendet werden können. Er rendert einfach nur HTML- und ignoriert ASP.NET- und SharePoint-Markup. SharePoint rendert nur ASP.NET- und SharePoint-Markup, ignoriert aber HTML.</span><span class="sxs-lookup"><span data-stu-id="c080a-p111">Design Manager generates HTML snippets that can be used by any web design tool—it just renders HTML and ignores ASP.NET and SharePoint markup. SharePoint renders only ASP.NET and SharePoint markup and ignores HTML.</span></span>
  
    
    

### <a name="device-channels"></a><span data-ttu-id="c080a-152">Gerätekanäle</span><span class="sxs-lookup"><span data-stu-id="c080a-152">Device channels</span></span>

<span data-ttu-id="c080a-p112">Im Entwurfs-Manager erstellen Sie  [Gerätekanäle](sharepoint-design-manager-device-channels.md) und ordnet diese dann mobilen Geräten oder Browsern mithilfe von Teilzeichenfolgen der einzelnen auf dem Gerät eingehenden Zeichenfolge des Benutzer-Agenten zu. Ein Gerät kann zu mehreren Kanälen gehören, und die Kanäle können somit eine Rangordnung haben. Beispiel: Wenn Sie Gerätekanäle für "Smartphones" und "Windows Phone 8" erstellen, können Sie die Kanäle ordnen, so dass die Geräte, mit Windows Phone 8 ausgeführt werden, einen speziell für sie reservierten Kanal bekommen, während andere Smartphones zum "Smartphones"-Kanal zugeordnet werden.</span><span class="sxs-lookup"><span data-stu-id="c080a-p112">In Design Manager, you create  [device channels](sharepoint-design-manager-device-channels.md), and then you map them to mobile devices or browsers by using substrings of each incoming device's user agent string. A device can belong to multiple channels, so channels can be ranked. For example, if you create device channels for "smart phones" and "Windows Phone 8", you can rank the channels so that devices running Windows Phone 8 get the channel specifically assigned to them, while all other smart phones get content associated with the "smart phones" channel.</span></span>
  
    
    
<span data-ttu-id="c080a-p113">Nachdem Sie die Kanäle festgelegt haben, ordnen Sie dem Kanal eine Masterseite zu. Diese Masterseite verweist auf eine andere CSS-Datei als die Masterseite für den Standardkanal. Alle von Ihnen erstellten Seitenlayouts arbeiten mit alle von Ihnen erstellten Kanälen zusammen. Wenn Sie die Seitenlayoutentwürfe bei den Kanälen unterschiedlich entwerfen möchten, verwenden Sie das Steuerelement **Gerätekanalbereich**.</span><span class="sxs-lookup"><span data-stu-id="c080a-p113">After you define channels, map a master page to each one. This master page can reference a different CSS file than the master page for the default channel. All page layouts that you create will work with all of the channels that you create; to differentiate page layout designs between channels, use the **Device Channel Panel** control.</span></span>
  
    
    
<span data-ttu-id="c080a-p114">Veröffentlichungssites in SharePoint sind für eine mobile Entwicklung optimiert. Sie können mit dem Gerätekanalfeature Kanäle für mindestens ein Gerät definieren, um Ihnen eine Kontrolle darüber zu geben, wie Mobilgerätbenutzer die Benutzerfreundlichkeit Ihrer Website erfahren. Für eine bessere Optik, können Sie den einzelnen Kanälen eine alternative Masterseite zuweisen. Wählen Sie, ob Sie Teile eines Seitenlayouts in einen Kanal mit ein- oder ausschließen möchten, und sehen Sie in der Vorschau, wie der mobile Kanalentwurf während der Entwicklung fortschreitet. Gerätekanäle werden vor dem Hintergrund einer Suchmaschinenoptimierung (SEO) geplant. Passen Sie damit Look and Feel der vorhandenen Seiten an, um mobile Szenarien zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p114">Publishing sites in SharePoint are optimized for mobile development. You can use the device channels feature to define channels for one or more devices—giving you finely-tuned control over how mobile users experience your site. You can assign an alternate master page to each channel, giving it a unique chrome. You can choose to include or exclude portions of any page layout in a channel and preview how mobile channel design is progressing while it is being developed. Device channels are designed with search engine optimization (SEO) in mind. You can use them to transform the look and feel of existing pages to support mobile scenarios.</span></span>
  
    
    
<span data-ttu-id="c080a-p115">Sie können Kanäle dafür einsetzen, dass bestimmte Renderings auf bestimmten Geräten erschienen; dies wird Kanäle erzwingen genannt. Dies ist bei mobilen Szenarien nützlich, wenn Sie ein Rendering geplant haben, das für ein bestimmtes mobiles Gerät optimiert ist.</span><span class="sxs-lookup"><span data-stu-id="c080a-p115">You can use channels to force specific renderings to appear on specific devices—this is called forcing channels. This is useful in mobile scenarios where you have defined a rendering that is optimal for a specific mobile device.</span></span>
  
    
    

### <a name="device-channel-panel-control"></a><span data-ttu-id="c080a-167">Steuerelement "Gerätekanalbereich"</span><span class="sxs-lookup"><span data-stu-id="c080a-167">Device Channel Panel control</span></span>

<span data-ttu-id="c080a-p116">"Gerätekanalbereich" ist ein neues Steuerelement, das Sie in das Seitenlayout mit aufnehmen können, um zu steuern, welche Inhalte in welchem Kanal gerendert werden sollen. Der Gerätekanalbereich ist ein Container, der einem oder mehreren Kanälen zugeordnet ist: Wenn mindestens einer dieser Kanäle während des Renderings der Seite aktiv ist, werden alle Inhalte des Gerätekanalbereichs gerendert. Über "Gerätekanalbereich" können Sie festlegen, wann ein bestimmter Inhalt für bestimmte Kanäle mit eingeschlossen werden soll.</span><span class="sxs-lookup"><span data-stu-id="c080a-p116">The Device Channel Panel is a new control that you can include in a page layout to control what content is rendered in which channel. The Device Channel Panel is a container that is mapped to one or more channels: If one or more of those channels are active when the page is rendered, all of the contents of the Device Channel Panel are rendered. The Device Channel Panel helps you determine when to include specific content for specific channels.</span></span>
  
    
    

### <a name="display-templates"></a><span data-ttu-id="c080a-171">Anzeigevorlagen</span><span class="sxs-lookup"><span data-stu-id="c080a-171">Display templates</span></span>
<span data-ttu-id="c080a-172"><a name="SP15_BuildSitesForSP2013_DisplayTemplates"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-172"></span></span>

<span data-ttu-id="c080a-p117">Sie möchten möglicherweise Format und Darstellung der Suchergebnisse auf Ihrer Website steuern können. Verwenden Sie dazu Anzeigevorlagen, die die verfügbaren Optionen einer Anpassung der Suchergebnisse über die Benutzeroberfläche über die Zuordnung der anzuzeigenden vordefinierten Felder hinaus erweitern.</span><span class="sxs-lookup"><span data-stu-id="c080a-p117">You may want to control the format and presentation of search results on your website. You can do that using display templates, which extend the options available for customizing search results through the user interface beyond mapping the predefined fields that you want to display.</span></span>
  
    
    
<span data-ttu-id="c080a-p118">Es gibt drei Kontexte, wenn Sie Anzeigevorlagen mit Suchergebnissen verwenden möchten: eine Darstellungszuordnung der Gesamtstruktur der Suchergebnisse, eine Darstellung von gruppierten Ergebnissen und eine Darstellung der einzelnen Ergebnisse oder Elemente im Resultset. Diese Darstellungsarten werden "Steuerelementvorlage", "Gruppenvorlage" und "Elementvorlage" genannt.</span><span class="sxs-lookup"><span data-stu-id="c080a-p118">There are three contexts when you may want to use display templates with search results—when you want to map how the overall structure of search results are presented, when you want to show groups of results, and when you want to show how each result, or item, in the result set is displayed. These are called Control, Group, and Item templates, respectively.</span></span>
  
    
    
<span data-ttu-id="c080a-177">Weitere Informationen zu Anzeigevorlagen finden Sie unter  [Anzeigevorlagen im SharePoint-Entwurfs-Manager](sharepoint-design-manager-display-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c080a-177">To learn more about display templates, see  [SharePoint Design Manager display templates](sharepoint-design-manager-display-templates.md).</span></span>
  
    
    

### <a name="image-renditions"></a><span data-ttu-id="c080a-178">Bilddarstellungen</span><span class="sxs-lookup"><span data-stu-id="c080a-178">Image renditions</span></span>
<span data-ttu-id="c080a-179"><a name="SP15_BuildSitesForSP2013_DisplayTemplates"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-179"></span></span>

<span data-ttu-id="c080a-p119">Mit  [Bildwiedergaben](sharepoint-design-manager-image-renditions.md) können Sie hochgeladene Bilder in vordefinierten Größen, Breiten und Beschnitten anzeigen. Sie können mehrere Wiedergaben ein und derselben Quellbilddatei erstellen. Das heißt, Sie können die Anzeigemerkmale einmal festlegen und sie dann auf eine beliebige Anzahl Bilder anwenden. Beispiel: Eine Bildwiedergabe namens **Article_image** zeigt ein Bild in Vollbildgröße in einem Artikel an, während die Wiedergabe namens **Thumbnail_small** eine kleinere Version des Bildes in einem von Ihnen definierten Kontext anzeigt.</span><span class="sxs-lookup"><span data-stu-id="c080a-p119">You can use  [image renditions](sharepoint-design-manager-image-renditions.md) to display uploaded images in predefined sizes, widths, and crops. You can create more than one rendition of a source image file, which means that you can set the display characteristics once and apply them to any number of images. For example, a rendition named **Article_image** displays a full-sized image in an article, while the rendition named **Thumbnail_small** displays a smaller version of the image in a context that you define.</span></span>
  
    
    
<span data-ttu-id="c080a-p120">Bevor Sie Bildwiedergaben verwenden können, stellen Sie sicher, dass der BLOB-Cache auf dem Server aktiviert ist. Dies erfolgt über in den Internetinformationsdiensten (IIS) mit den Verwaltungstools. Suchen Sie dort nach der **web.config**-Datei, und aktivieren Sie den BLOB-Cache. Aktualisieren Sie die Seite, damit die Bildwiedergaben verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="c080a-p120">Before you can use image renditions, ensure that the BLOB cache is enabled on the server, which you can do in the Administration tools in Internet Information Services (IIS). Find your **web.config** file there and enable the BLOB cache. Refresh the page, and image renditions will be available.</span></span>
  
    
    

## <a name="managed-metadata-and-navigation-in-sharepoint"></a><span data-ttu-id="c080a-186">Verwaltete Metadaten und Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c080a-186">Managed metadata and navigation in SharePoint</span></span>
<span data-ttu-id="c080a-187"><a name="SP15_WhatsNewSiteDevelopment_MetadataAndNavigation"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-187"></span></span>

<span data-ttu-id="c080a-188">Die in eingeführten Enterprise-Managed-Metadaten-Funktionen (EMM) wurden in SharePoint für mehr Leistung, leichteren Zugriff über die Benutzeroberfläche und taxonomiegesteuerte Navigation, die so genannte verwaltete Navigation, verbessert und erweitert.</span><span class="sxs-lookup"><span data-stu-id="c080a-188">Enterprise managed metadata (EMM) capabilities introduced in are improved and extended in SharePoint for better performance, easier access through the UI, and taxonomy-driven navigation—called managed navigation.</span></span>
  
    
    

### <a name="managed-navigation"></a><span data-ttu-id="c080a-189">Verwaltete Navigation</span><span class="sxs-lookup"><span data-stu-id="c080a-189">Managed navigation</span></span>

<span data-ttu-id="c080a-p121">Verwaltete Navigation ist die taxonomiegesteuerte Alternative zur herkömmlichen SharePoint-Navigationsfunktion, der strukturierten Navigation, die auf den SharePoint-Strukturen basiert. Die Funktion der  [verwalteten Navigation](managed-navigation-in-sharepoint.md) ermöglicht Ihnen den Entwurf einer Websitenavigation, die über verwaltete Metadaten gesteuert wird. Verwalte Navigation erstellt SEO-optimierte URLs, die aus der verwalteten Navigationsstruktur abgeleitet werden. Da die verwaltete Navigation taxonomisch gesteuert wird, können Sie diese für den Entwurf der Websitenavigation in wichtigen Geschäftskonzepten verwenden, ohne die Struktur Ihrer Website oder Websitekomponenten ändern zu müssen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p121">Managed navigation is the taxonomy-based alternative to the traditional SharePoint navigation feature—called structured navigation—that is based on the structure of SharePoint. The  [managed navigation](managed-navigation-in-sharepoint.md) feature enables you to design a site navigation that is driven by managed metadata. Managed navigation creates SEO-friendly URLs that are derived from the managed navigation structure. Because managed navigation is driven by taxonomy, you can use it to design site navigation around important business concepts without changing the structure of your sites or site components.</span></span>
  
    
    

### <a name="content-search-web-part"></a><span data-ttu-id="c080a-194">Webpart für Inhaltssuche</span><span class="sxs-lookup"><span data-stu-id="c080a-194">Content Search Web Part</span></span>
<span data-ttu-id="c080a-195"><a name="SP15_BuildSitesForSP2013_ContentSearchWebPart"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-195"></span></span>

<span data-ttu-id="c080a-p122">Mit dem  [Inhaltssuche-Webpart (CSWP)](content-search-web-part-in-sharepoint.md) können Sie Suchdaten auf Ihren Seiten anzeigen. Der Webpart hat eine ähnliche Funktion wie die des Webparts für Inhaltsabfragen, aber seine Websitedesignziele sind andere. CSWP-Formatvorlagen können leichter angepasst werden als CQWP-Formatvorlagen. CSWP gibt clientseitige Ergebnisse im JSON-Format zurück. Sie können auf dem Server Ergebnisse mithilfe von Anzeigevorlagen anpassen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p122">You can use the  [Content Search Web Part (CSWP)](content-search-web-part-in-sharepoint.md) to display search data on your pages. It serves a function similar to that of the Content Query Web Part, but it serves different site design goals. CSWP styles are easier to customize than Content Query Web Part styles. CSWP returns client-side results in JSON format. On the server, you can customize results by using display templates.</span></span>
  
    
    

### <a name="other-managed-metadata-improvements-for-sites"></a><span data-ttu-id="c080a-201">Weitere verwaltete Metadatenverbesserungen für Websites</span><span class="sxs-lookup"><span data-stu-id="c080a-201">Other managed metadata improvements for sites</span></span>
<span data-ttu-id="c080a-202"><a name="SP15_BuildSitesForSP2013_ContentSearchWebPart"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-202"></span></span>

<span data-ttu-id="c080a-p123">SharePoint führt mehrere Verbesserungen bei verwalteten Metadaten-Benutzeroberflächen und Funktionen ein. Weitere Informationen finden Sie unter  [Verwaltete Metadaten und Navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c080a-p123">SharePoint introduces several improvements to the managed metadata UI and functionality. To learn more, see  [Managed metadata and navigation in SharePoint](managed-metadata-and-navigation-in-sharepoint.md).</span></span>
  
    
    

## <a name="publishing-content-in-sharepoint"></a><span data-ttu-id="c080a-205">Veröffentlichung von Inhalten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c080a-205">Publishing content in SharePoint</span></span>
<span data-ttu-id="c080a-206"><a name="SP15_WhatsNewSiteDevelopment_Publishing"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-206"></span></span>

<span data-ttu-id="c080a-207">SharePoint bietet neue Features für das Veröffentlichen von Inhalten, mit denen Sie Veröffentlichungssites entwerfen können, die wiederum neue, flexiblere und komplexere Topologien und Szenarien unterstützen.</span><span class="sxs-lookup"><span data-stu-id="c080a-207">SharePoint offers new content publishing features that enable you to develop publishing sites that support new, more flexible, and more complex topologies and scenarios.</span></span> 
  
    
    

### <a name="design-packages"></a><span data-ttu-id="c080a-208">Designpakete</span><span class="sxs-lookup"><span data-stu-id="c080a-208">Design packages</span></span>

<span data-ttu-id="c080a-p124">Wenn Sie ein erfahrener Webdesigner sind, möchten Sie vielleicht einen Entwurf in Ihrer eigenen Umgebung oder Websitesammlung erstellen und testen, bevor er in anderen Websitesammlungen installiert wird. Sollten Sie die websiteübergreifende Veröffentlichung zum Teilen von Inhalten in allen Websitesammlungen verwenden, können Sie denselben Entwurf als Paket auf jeder Website installieren.</span><span class="sxs-lookup"><span data-stu-id="c080a-p124">If you're a professional web designer, you may want to create and test a design in your own environment or site collection before handing it off to install in other site collections. If you're using cross-site publishing to share content across site collections, you may want to package and install the same design on each site.</span></span>
  
    
    
<span data-ttu-id="c080a-p125">In früheren SharePoint-Versionen mussten Sie, wenn Sie einen Entwurf erneut verwenden wollten, Visual Studio installiert haben, um ein SharePoint-Lösungspaket (.wsp-Datei) zu erstellen. Auf der Zielwebsite mussten Sie dann das Paket in den Lösungskatalog hochladen und dort ausführen. In SharePoint können Sie jetzt, nachdem Sie den Entwurf Ihrer Website abgeschlossen haben, im Entwurfs-Manager **Paket exportieren** wählen, um eine einzige .wsp-Datei, das so genannte [Designpaket](sharepoint-design-manager-design-packages.md) zu exportieren. Beim Export eines Designpakets erstellt SharePoint automatisch ein Designpaket des gesamten Inhalts, den Sie im Masterseitenkatalog, in der Formatbibliothek, in der Designgalerie, in der Gerätkanalliste und in den Seiteninhaltstypen hinzugefügt oder geändert haben.</span><span class="sxs-lookup"><span data-stu-id="c080a-p125">In previous versions of SharePoint, if you wanted to reuse a design, you had to use Visual Studio to create a SharePoint Solution Package (.wsp file). Then, in the destination site, you would upload the package to the Solutions Gallery and execute it. Now, in SharePoint, after you finish designing your site, you can choose **Export Package** in Design Manager to export a single .wsp file called a [design package](sharepoint-design-manager-design-packages.md). When you export a design package, SharePoint automatically packages all of the contents that you have added or changed in the Master Page Gallery, Style Library, Theme Gallery, the Device Channels list, and Page content types into a design package.</span></span> 
  
    
    

> <span data-ttu-id="c080a-215">**Hinweis:** Ein Designpaket enthält keine Seiten, Navigationseinstellungen oder den Terminologiespeicher.</span><span class="sxs-lookup"><span data-stu-id="c080a-215">**Note** A design package does not include pages, navigation settings, or the term store.</span></span> 
  
    
    

<span data-ttu-id="c080a-p126">Designpakete überschreiben bei öffentlichen Office 365-Websites keine vorhandenen Dateien Bei der Installation eines Designpakets wird ein neuer Ordner im Masterseitenkatalog, in der Formatbibliothek und in der Designgalerie erstellt, in der die Designelemente isoliert sind.</span><span class="sxs-lookup"><span data-stu-id="c080a-p126">For Office 365 public websites, design packages do not overwrite existing files. Installing a design package creates a new folder in the Master Page Gallery, Style Gallery, and Theme Gallery where design assets are isolated.</span></span> 
  
    
    
<span data-ttu-id="c080a-p127">Wenn Sie ein Designpaket importieren, überschreiben die Designelemente des Pakets vorhandene Dateien. Die Designelement werden dann auf das aktuelle Design der Website angewendet. Die Standard- und Systemmasterseite der Website, das Design und die alternative CSS-Datei sind alle in den Dateien im Designpaket festgelegt. Ein Entwurf, der in einer Umgebung erstellt wurde, kann mit Designpaketen problemlos auf andere, separate Umgebungen angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="c080a-p127">When you import a design package, the design assets in the package overwrite any existing files and are applied as the current design of the site. The site's default and system master page, theme, and alternate CSS are all set from the files in the design package. With design packages, a design built in one environment can easily be applied to another, separate environment.</span></span>
  
    
    

### <a name="catalogs"></a><span data-ttu-id="c080a-221">Kataloge</span><span class="sxs-lookup"><span data-stu-id="c080a-221">Catalogs</span></span>

<span data-ttu-id="c080a-p128">Websiteveröffentlichung in SharePoint führt Kataloge ein, mit deren Hilfe Sie Listen in Veröffentlichungssites einbinden können. Mit Katalogen können Inhalte in allen Websitesammlungen veröffentlicht werden. Die Funktionen der websiteübergreifenden Veröffentlichung hängen vom jeweiligen Katalog ab. Sie können Kataloge für eine Wiederverwendung von Inhalten auf allen Ihren Websites und grenzüberschreitend auf allen Ihren Intranetwebsites, Internetwebsites und Extranetwebsites verwenden. Kataloge sind bei vordefinierten Suchabfragen in der Suche gekennzeichnet. Sie können Inhalte in Katalogen in allen Websitesammlungen darstellen, wenn Sie dazu den [Inhaltssuche-Webpart (CSWP)](content-search-web-part-in-sharepoint.md) verwenden. Außerdem können Sie benutzerdefinierten Code schreiben, um Kataloge zu befüllen, einen Produktkatalog mit einer Seite verknüpfen und individuelle Seiten mit benutzerdefiniertem Seitenlayout, Webparts und HTML-Inhalten, die ausschließlich im festgelegten Kontext erscheinen, verbessern.</span><span class="sxs-lookup"><span data-stu-id="c080a-p128">SharePoint site publishing introduces catalogs, which enable you to incorporate lists into your publishing sites. Catalogs enable content to be published across site collections—the cross-site publishing features depend on catalogs. You can use catalogs to truly reuse content across your sites and across the boundary between your intranet sites, Internet sites, and extranet sites. For predefined search queries, catalogs are flagged in search. You can surface content stored in catalogs across site collections by using the  [Content Search Web Part (CSWP)](content-search-web-part-in-sharepoint.md). You can write custom code to populate catalogs, connect a product catalog to a site, and curate individual pages with custom page layouts, Web Parts, and HTML content that appears only in the defined context.</span></span>
  
    
    

### <a name="client-side-rendering-controls"></a><span data-ttu-id="c080a-228">Clientseitige Rendering-Steuerelemente</span><span class="sxs-lookup"><span data-stu-id="c080a-228">Client-side rendering controls</span></span>

<span data-ttu-id="c080a-p129">Alle neuen Steuerelemente in SharePoint werden clientseitig wiedergegeben. Als Designer oder Entwickler können Sie steuern, wie Inhalte auf der Seite wiedergegeben werden sollen. Sie können außerdem zahlreiche Designtechniken verwenden, um das gewünschte Erscheinungsbild und Verhalten auf den veröffentlichten Seiten zu erzielen, indem Sie Features wie Inhaltssuche-Webparts und Anzeigevorlagen mit einschließen. Daten werden in einem clientseitigen JSON-Array in die Steuerelemente geschrieben. Inhalte zeigen Sie über JavaScript, CSS und Vorlagen an.</span><span class="sxs-lookup"><span data-stu-id="c080a-p129">All new controls in SharePoint are rendered client-side. As a designer or a developer, you have control over how content is rendered on the page, and you can use various design techniques to get the look and behaviors you want on your published pages by using features including the Content Search Web Part and display templates. Data is written to the controls in a client-side JSON array, and you can display content using JavaScript, CSS, and templates.</span></span> 
  
    
    

### <a name="cross-site-publishing"></a><span data-ttu-id="c080a-232">Websiteübergreifende Veröffentlichung</span><span class="sxs-lookup"><span data-stu-id="c080a-232">Cross-site publishing</span></span>

<span data-ttu-id="c080a-p130">Microsoft SharePoint führt ein websiteübergreifendes Veröffentlichungsfeature ein, mit dem Sie Inhalte in mehreren Websitesammlungen wiederverwenden können. Es verwendet integrierte Suchfunktionen, um Szenarien und Architekturen veröffentlichen zu können. Zum ersten Mal können Sie jetzt Websites farmübergreifend in SharePoint erstellen. Damit überbrücken Ihre Websites die Kluft zwischen Intranet und Internet.</span><span class="sxs-lookup"><span data-stu-id="c080a-p130">Microsoft SharePoint introduces a cross-site publishing feature that enables you to reuse content across multiple site collections. It uses built-in search capabilities to enable publishing scenarios and architectures. For the first time, you can design sites that cross SharePoint farms—enabling your sites to span the boundary between intranets and the Internet.</span></span> 
  
    
    
<span data-ttu-id="c080a-p131">Verwenden Sie die Themenseitenfunktion, um die Benutzerfreundlichkeit der Startseite an Inhalte anzupassen, die websiteübergreifend veröffentlich werden. Verwenden Sie auch SEO-freundliche URLs für das Verwalten und eine leichtere Aufrechterhaltung der Websitestruktur in einer breiten Palette an Szenarien, einschließlich komplexer mehrsprachiger Websitetopologien.</span><span class="sxs-lookup"><span data-stu-id="c080a-p131">Use the topic pages feature to customize the landing page experience for content that is published across sites. Use SEO-friendly URLs to manage and more easily persist and maintain site structure across a broad range of scenarios—including complex multilingual site topologies.</span></span>
  
    
    
<span data-ttu-id="c080a-238">Weitere Informationen zur websiteübergreifenden Veröffentlichung finden Sie unter [Szenario: Erstellen von SharePoint-Websites mit websiteübergreifender Veröffentlichung in SharePoint](http://technet.microsoft.com/de-de/sharepoint/jj872721).</span><span class="sxs-lookup"><span data-stu-id="c080a-238">To learn more about cross-site publishing, see  [Scenario: Create SharePoint sites by using cross-site publishing in SharePoint Server 2013](http://technet.microsoft.com/de-de/sharepoint/jj872721). To learn more about development options for cross-site publishing, see  Cross-site publishing in SharePoint.</span></span> <span data-ttu-id="c080a-239">Weitere Informationen über Entwicklungsoptionen für die websiteübergreifende Veröffentlichung finden Sie unter [Websiteübergreifende Veröffentlichung in SharePoint](cross-site-publishing-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c080a-239">To learn more about cross-site publishing, see  Scenario: Create SharePoint sites by using cross-site publishing in SharePoint Server 2013. To learn more about development options for cross-site publishing, see  [Cross-site publishing in SharePoint](cross-site-publishing-in-sharepoint.md).</span></span>
  
    
    

### <a name="seo-enhancements"></a><span data-ttu-id="c080a-240">SEO-Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="c080a-240">SEO enhancements</span></span>

<span data-ttu-id="c080a-p133">Viele Benutzer von Geschäftswebsites werden von großen Suchmaschinen wie Bing und seine Konkurrenten zu Geschäftswebsites im Internet umgeleitet. SharePoint umfasst Features, wie benutzerfreundliche URLs, Homepageumleitung, XML-Sitemaps, benutzerdefinierte SEO-Eigenschaften, mit denen Sie flexibel Browsertitel, **<Meta>**-Tagbeschreibungen, Schlüsselwörter und leichtverständliche URLs für mehrsprachige Websitevarianten festlegen können.</span><span class="sxs-lookup"><span data-stu-id="c080a-p133">Many business site users are referred to Internet business sites from large search engines like Bing and its global competitors. SharePoint includes features like friendly URLs, home page redirects, XML sitemaps, custom SEO properties that enable you to flexibly define the browser title and **<Meta>** tag descriptions and keywords, and easier-to-understand URLs for multilingual site variations.</span></span>
  
    
    
<span data-ttu-id="c080a-p134">In Office 365 generiert die Websiteinfrastruktur innerhalb von 24 Stunden nach einer Websiteänderung eine aktualisierte XML-Sitemap. Dank der lokalen Installation können Sie die Aktualität Ihrer Sitemaps anpassen und festlegen, welche Suchmaschinen Microsoft für Sie pingen soll, wenn die Sitemap aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="c080a-p134">In Office 365, the site infrastructure generates an updated XML sitemap for you within 24 hours of a site change. With an on-premises installation, you can tune the freshness of your sitemaps and specify which search engines you want Microsoft to ping when we update the sitemap.</span></span>
  
    
    
<span data-ttu-id="c080a-p135">Das, was Ihre Freunde auf Facebook mögen, beeinflusst das, was Sie in den von Bing und anderen Suchmaschinen zurückgegebenen Suchergebnissen sehen. Sie können APIs in SharePoint-Programmierungsmodellen verwenden, um eine Suchoptimierung für Ihre Website anzupassen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p135">What your friends like on Facebook affects what you see in the search results returned by Bing and other large search engines. You can use APIs in SharePoint programming models to customize how search is optimized for your site.</span></span>
  
    
    

### <a name="analytics-and-recommendations"></a><span data-ttu-id="c080a-247">Analyse und Empfehlungen</span><span class="sxs-lookup"><span data-stu-id="c080a-247">Analytics and recommendations</span></span>

<span data-ttu-id="c080a-p136">Sie können nachverfolgen, wie Personen Veröffentlichungswebsites und deren Komponenten unter Zuhilfenahme des SharePoint Analytics-Features nutzen, das tief in die Suchmaschine integriert ist. Analytics befördert die Empfehlungsmöglichkeiten bei Inhalten und führt Berechnungen als verwaltete Eigenschaften in den Suchindex ein. Die Empfehlungen von Suchanalysen, wie Seitenaufrufe und eindeutige Elemente pro Tag, beeinflussen die Relevanz von Suchergebnissen.</span><span class="sxs-lookup"><span data-stu-id="c080a-p136">You can track how people use publishing sites and their components using the SharePoint analytics feature, which is deeply integrated with the search engine. Analytics drives recommendations capabilities on content, and injects calculations into the search index as managed properties. The recommendations provided by search analytics, which include page views and unique items per day, can influence the relevance of search results.</span></span>
  
    
    
<span data-ttu-id="c080a-p137">Analytics anonymisiert Daten und macht alle 2 Wochen ein Rollup. Analytics löscht erst alle 2 Wochen, dann nach 3 Jahren jeden Monat, Ereignisse. Lebensdaueransichten bleiben immer erhalten. Der zuletzt angezeigte Inhalt wird zunächst geglättet, bevor Analytics Aggregatdaten in eine Berichtsdatenbank verschiebt. Für den Export von Daten aus der Berichtsdatenbank in Excel, für das Anpassen der Gewichtung von **View**-Ereignissen und für das Erstellen von benutzerdefinierten Ereignissen, einschließlich jener, die von JavaScript bereitgestellt werden, können Sie benutzerdefinierten Code verwenden.</span><span class="sxs-lookup"><span data-stu-id="c080a-p137">Analytics makes data anonymous and rolls it up every 15 days. Analytics purges events every 15 days and then monthly after 3 years. Lifetime views are always retained. The least-visited content is trimmed before analytics pushes aggregate data to a reporting database. You can use custom code to export data to Excel from the reporting database, customize the weight of the **View** event, and create custom events—including those submitted by JavaScript.</span></span>
  
    
    

### <a name="variations-and-multilingual-sites"></a><span data-ttu-id="c080a-256">Variationen und mehrsprachige Websites</span><span class="sxs-lookup"><span data-stu-id="c080a-256">Variations and multilingual sites</span></span>

<span data-ttu-id="c080a-257">Sie können das Variationsfeature in SharePoint verwenden, um mehrsprachige Websites oder andere Websites zu erstellen, auf denen Sie die Präsentation Ihrer Inhalte variieren möchten.</span><span class="sxs-lookup"><span data-stu-id="c080a-257">You can use the variations feature in SharePoint to create multilingual sites or other sites where you want to vary the presentation of your content.</span></span> <span data-ttu-id="c080a-258">Das Variationsfeature ist auf eine Websitesammlung beschränkt.</span><span class="sxs-lookup"><span data-stu-id="c080a-258">The variations feature is constrained to one site collection.</span></span> <span data-ttu-id="c080a-259">Das heißt, Sie können für eine Quellsprache/ein Quellgebietsschema mehrere Zielsprachen-/-gebietsschema-Varianten als aktuelle Websites innerhalb der gleichen SharePoint-Websitesammlung erstellen.</span><span class="sxs-lookup"><span data-stu-id="c080a-259">That is, you can create target language/locale "variants" of a source language/locale as current websites within the same SharePoint site collection.</span></span> <span data-ttu-id="c080a-260">Variationen unterstützen benutzerfreundliche URLs sowie die Möglichkeit zum Exportieren oder Importieren von Inhalten für die Übersetzung durch einen Drittanbieter im [XLIFF-Dateiformat](the-xliff-interchange-file-format-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="c080a-260">Variations supports friendly URLs and the ability to export or import content for translation by a third party in  [XLIFF file format](the-xliff-interchange-file-format-in-sharepoint.md).</span></span> <span data-ttu-id="c080a-261">Sie können Bezeichnungen, eine Seite für Übersetzung und Replikation, eine Vielzahl von Listenelementen (z. B. Dokumentbibliotheken.md) und Navigation in die Exportpakete einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="c080a-261">You can include labels, a page for translation and replication, a variety of list items (for example, document libraries.md), and navigation in your export packages.</span></span> 
  
    
    

## <a name="additional-resources"></a><span data-ttu-id="c080a-262">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="c080a-262">Additional resources</span></span>
<span data-ttu-id="c080a-263"><a name="SP15_WhatsNewSiteDevelopment_AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="c080a-263"></span></span>


-  [<span data-ttu-id="c080a-264">Ausführen grundlegender Vorgänge unter Verwendung von SharePoint-Clientbibliothekscode</span><span class="sxs-lookup"><span data-stu-id="c080a-264">Complete basic operations using SharePoint client library code</span></span>](http://msdn.microsoft.com/library/5a69c9e3-73bf-4ed5-bc19-182056bdb394%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c080a-265">Ausführen grundlegender Vorgänge unter Verwendung von JavaScript-Bibliothekscode in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c080a-265">Complete basic operations using JavaScript library code in SharePoint</span></span>](http://msdn.microsoft.com/library/29089af8-dbc0-49b7-a1a0-9e311f49c826%28Office.15%29.aspx)
    
  
-  [<span data-ttu-id="c080a-266">Vorgehenweise: Anpassen der Seitenlayouts für eine katalogbasierte Website in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c080a-266">How to: Customize page layouts for a catalog-based site in SharePoint</span></span>](how-to-customize-page-layouts-for-a-catalog-based-site-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c080a-267">Vorgehensweise: ändern die Vorschauseite in SharePoint-Design-Manager</span><span class="sxs-lookup"><span data-stu-id="c080a-267">How to: Change the preview page in SharePoint Design Manager</span></span>](how-to-change-the-preview-page-in-sharepoint-design-manager.md)
    
  
-  [<span data-ttu-id="c080a-268">Vorgehensweise: Beheben von Fehlern und Warnungen bei der Vorschau einer Seite in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c080a-268">How to: Resolve errors and warnings when previewing a page in SharePoint</span></span>](how-to-resolve-errors-and-warnings-when-previewing-a-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c080a-269">Übersicht über Designs für SharePoint</span><span class="sxs-lookup"><span data-stu-id="c080a-269">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md)
    
  
-  [<span data-ttu-id="c080a-270">Verwaltete Metadaten und Navigation in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c080a-270">Managed metadata and navigation in SharePoint</span></span>](managed-metadata-and-navigation-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c080a-271">What's new in SharePoint-Suche für Entwickler</span><span class="sxs-lookup"><span data-stu-id="c080a-271">What's new in SharePoint search for developers</span></span>](what-s-new-in-sharepoint-search-for-developers.md)
    
  

