---
title: Codeausschnitte des SharePoint-Entwurfs-Managers
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 68caef4c-5941-4a88-b34b-f88122801cef
ms.openlocfilehash: 2c670d8fb7cd6ec3f293a3e5da9b75380005f598
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="sharepoint-design-manager-snippets"></a><span data-ttu-id="c9b6c-102">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="c9b6c-102">SharePoint Design Manager snippets</span></span>
<span data-ttu-id="c9b6c-p101">Ein Codeausschnitt ist eine HTML-Darstellung einer SharePoint-Komponente oder eines Steuerelements, wie beispielsweise eine Navigationsleiste oder ein Webpart. Mithilfe des Codeausschnittkatalogs im Entwurfs-Manager können Sie Ihrer HTML-Gestaltungsvorlage oder dem Seitenlayout schnell SharePoint-Funktionen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p101">A snippet is an HTML representation of a SharePoint component or control such as a navigation bar or a Web Part. By using the Snippet Gallery in Design Manager, you can quickly add SharePoint functionality to your HTML master page or page layout.</span></span>
## <a name="introduction-to-snippets-and-the-snippet-gallery"></a><span data-ttu-id="c9b6c-105">Einführung in Codeausschnitte und den Codeausschnittkatalog</span><span class="sxs-lookup"><span data-stu-id="c9b6c-105">Introduction to snippets and the Snippet Gallery</span></span>
<span data-ttu-id="c9b6c-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="c9b6c-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="c9b6c-p102">Nachdem Sie eine Gestaltungsvorlage konvertiert oder ein Seitenlayout erstellt haben, verfügen Sie über eine HTML-Version der betreffenden Seite. Über den Codeausschnittkatalog können Sie der HTML-Datei, die der Gestaltungsvorlage oder dem Seitenlayout zugeordnet ist, schnell bestimmte SharePoint-Funktionen, wie Such-, Navigations- oder Gerätekanalbereiche hinzufügen. Der Codeausschnittkatalog ist eine Seite im Entwurfs-Manager, auf der Sie folgende Möglichkeiten haben:</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p102">After you convert a master page or create a page layout, you have an HTML version of that page. With the Snippet Gallery, you can quickly add specific SharePoint functionality, such as search or navigation or device channel panels, to the HTML file associated with your master page or page layout. The Snippet Gallery is a page in Design Manager where you can:</span></span>
  
    
    

- <span data-ttu-id="c9b6c-110">Auswählen einer SharePoint-Komponente aus den im Menüband verfügbaren Komponenten</span><span class="sxs-lookup"><span data-stu-id="c9b6c-110">Choose a SharePoint component from those available on the ribbon.</span></span>
    
  
- <span data-ttu-id="c9b6c-111">Konfigurieren der Eigenschaften für diese Komponente</span><span class="sxs-lookup"><span data-stu-id="c9b6c-111">Configure the properties for that component.</span></span>
    
  
- <span data-ttu-id="c9b6c-112">Anzeigen einer Vorschau im Browser</span><span class="sxs-lookup"><span data-stu-id="c9b6c-112">Preview its appearance in the browser.</span></span>
    
  
- <span data-ttu-id="c9b6c-113">Kopieren des HTML-Codeausschnitts in die Zwischenablage, damit Sie den Codeausschnitt an der gewünschten Stelle in der HTML-Datei einfügen können</span><span class="sxs-lookup"><span data-stu-id="c9b6c-113">Copy the HTML code snippet to the Clipboard so that you can paste the snippet at the location you want in the HTML file.</span></span>
    
  
<span data-ttu-id="c9b6c-p103">Im Menüband werden verschiedene Optionen des Codeausschnittkatalogs angezeigt, je nachdem, ob Sie eine Gestaltungsvorlage oder ein Seitenlayout bearbeiten. Beispielsweise werden Navigationssteuerelemente nur für Gestaltungsvorlagen angezeigt, und Webpartzonen und Seitenfeld-Steuerelemente werden nur für Seitenlayouts angezeigt. Wenn Sie ein Seitenlayout bearbeiten, richten sich die verfügbaren Seitenfelder zudem nach dem Inhaltstyp des Seitenlayouts, das Sie bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p103">The Snippet Gallery displays different options on the ribbon, depending on whether you're editing a master page or page layout—for example, navigation controls are displayed only for master pages, and Web Part zones and page field controls are displayed only for page layouts. Also, when you are editing a page layout, the page fields that are available depend on the content type of the page layout that you're editing.</span></span>
  
    
    
<span data-ttu-id="c9b6c-p104">Nachdem Sie einen Codeausschnitt in die HTML-Datei eingefügt haben, erhalten Sie eine Vorschau des im Codeausschnitt angegebenen HTML-Codes zur Entwurfszeit. Sie können auch über die serverseitige Vorschau im Entwurfs-Manager sehen, wie das Steuerelement auf der Livewebsite dargestellt wird. Die Vorschau zur Entwurfszeit enthält möglicherweise statische Beispieldaten, während in der serverseitigen Vorschau ggf. verfügbare Livedaten verwendet werden. Bei einem Navigationssteuerelement, das Navigationslinks aus einem Ausdruckssatz bezieht, werden diese Ausdrücke in der serverseitigen Vorschau dynamisch angezeigt. Die Vorschau zur Entwurfszeit hingegen enthält eine statische Momentaufnahme der Ausdrücke zu dem Zeitpunkt der Erstellung des Codeausschnitts. Livedaten sind in der serverseitigen Vorschau für einige Codeausschnitte, darunter zahlreiche Webparts, nicht verfügbar. In einem solchen Fall erhalten Sie in der serverseitigen Vorschau die Meldung **Vorschau nicht verfügbar**.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p104">After you paste a snippet into your HTML file, you get a design-time preview from the HTML provided in the snippet. You can also use the server-side preview in Design Manager to see how the control will appear on the live site. The design-time preview may include static sample data, but the server-side preview uses live data, if available. For example, a navigation control that draws navigation links from a term set will display those terms dynamically in the server-side preview, but the design-time preview will have a static snapshot of the terms at the time you created the snippet. Live data is not available in the server-side preview for some snippets, however, including many Web Parts. In this case, the server-side preview may say **Preview Not Available**.</span></span>
  
> [!NOTE]
> <span data-ttu-id="c9b6c-p105">Ein Codeausschnitt enthält HTML-Code, über den Sie im HTML-Editor eine Vorschau zur Entwurfszeit erhalten. Der HTML-Code in den Kommentaren "Vorschau starten" und "Vorschau beenden" sollte jedoch nicht bearbeitet werden, da er sich nur auf die Vorschau zur Entwurfszeit auswirkt und nicht darauf, wie SharePoint den Codeausschnitt letztlich rendert. Zum Gestalten des Codeausschnitts müssen Sie stattdessen in der Regel die auf den Codeausschnitt angewendeten standardmäßigen SharePoint-Formatvorlagen ermitteln und außer Kraft setzen.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p105">A snippet contains HTML markup that gives you a design-time preview in your HTML editor, but the HTML markup contained in "start preview" and "end preview" comments should not be edited because it affects only the design-time preview, not how SharePoint ultimately renders that snippet. Instead, to style your snippet, you typically have to identify and override the default SharePoint styles that are applied to the snippet.</span></span> 
  
    
    


  
    
    

## <a name="insert-a-snippet-from-the-snippet-gallery"></a><span data-ttu-id="c9b6c-124">Einfügen eines Codeausschnitts aus dem Codeausschnittkatalog</span><span class="sxs-lookup"><span data-stu-id="c9b6c-124">Insert a snippet from the Snippet Gallery</span></span>
<span data-ttu-id="c9b6c-125"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="c9b6c-125"><a name="InsertSnippet"> </a></span></span>

<span data-ttu-id="c9b6c-p106">Im Codeausschnittkatalog werden verschiedene Optionen angezeigt. Dies richtet sich nach der Datei, die Sie bearbeiten. Beispielsweise sind für verschiedene Seitenlayouts verschiedene Gruppen von Seitenfeldern verfügbar. Um zum Codeausschnittkatalog zu navigieren, müssen Sie daher zunächst eine Gestaltungsvorlage oder ein Seitenlayout auswählen, die bzw. das bearbeitet werden soll.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p106">The Snippet Gallery displays different options depending on the file that you're editing. For example, different page layouts have different sets of page fields available to them. For this reason, to navigate to the Snippet Gallery, you must first select a master page or page layout to edit.</span></span>
  
    
    

### <a name="to-insert-a-snippet"></a><span data-ttu-id="c9b6c-129">So fügen Sie einen Codeausschnitt ein</span><span class="sxs-lookup"><span data-stu-id="c9b6c-129">To insert a snippet</span></span>


1. <span data-ttu-id="c9b6c-130">Wechseln Sie zu Ihrer Veröffentlichungswebsite.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-130">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="c9b6c-131">Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-131">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="c9b6c-132">Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten** oder **Seitenlayouts bearbeiten** aus, je nachdem, welchen Dateityp Sie bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-132">In Design Manager, in the left navigation pane, choose **Edit Master Pages** or **Edit Page Layouts**, depending on what type of file you're editing.</span></span>
    
  
4. <span data-ttu-id="c9b6c-133">Wählen Sie den Namen der Gestaltungsvorlage oder des Seitenlayouts aus, der bzw. dem Sie Codeausschnitte hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-133">Select the name of the master page or page layout that you want to add snippets to.</span></span>
    
  
5. <span data-ttu-id="c9b6c-134">Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-134">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="c9b6c-135">Wählen Sie im Menüband auf der Registerkarte **Entwurf** den Codeausschnitt aus, den Sie der Seite hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-135">On the ribbon, on the **Design** tab, choose the snippet that you want to add to your page.</span></span>
    
    <span data-ttu-id="c9b6c-136">Wenn Sie einen Codeausschnitt auswählen, wird der Codeausschnittkatalog aktualisiert. Auf der Seite werden dann eine Vorschau des Codeausschnitts, die für den Codeausschnitt verfügbaren Eigenschaften sowie der HTML-Codeausschnitt, den Sie in die HTML-Gestaltungsvorlage oder das Seitenlayout kopieren können, angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-136">When you select a snippet, the Snippet Gallery refreshes so that the page shows you a preview of that snippet, the properties available for that snippet, and the HTML code snippet that you can copy into your HTML master page or page layout.</span></span>
    
  
7. <span data-ttu-id="c9b6c-137">Klicken Sie auf der rechten Seite des Codeausschnittkatalogs unter **Infos zu dieser Komponente** auf Abschnittsüberschriften, oder wählen Sie diese aus, um Gruppen von Eigenschaften zu erweitern oder zu reduzieren und anschließend alle gewünschten benutzerdefinierten Eigenschaften zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-137">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
    <span data-ttu-id="c9b6c-p107">Die Eigenschaften, die für den Hauptzweck des Codeausschnitts am wichtigsten sind, werden im obersten Abschnitt mit der Bezeichnung "Wichtig" angezeigt. Dies sind die wesentlichen Eigenschaften, die Sie verstehen müssen, wenn Sie Codeausschnitte verwenden.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p107">The properties that are most important for the core purpose of the snippet appear in the top section named Important. These are the key properties that you have to understand when using a snippet.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c9b6c-140">Wenn das Eigenschaftenraster über eine Kopfzeile verfügt, die mit AjaxDelta endet, sollten Sie diese Eigenschaften ignorieren, da sie für die Steuerelemente im Zusammenhang mit der minimalen Downloadstrategie gelten, die für Gestaltungsvorlagen und Seitenlayouts, die über den Entwurfs-Manager erstellt werden, deaktiviert ist.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-140">If the property grid has a header that ends with AjaxDelta, you should ignore those properties because they apply to the controls related to the Minimal Download Strategy, which is disabled for master pages and page layouts created through Design Manager.</span></span> 

8. <span data-ttu-id="c9b6c-p108">Wählen Sie nach dem Konfigurieren von Eigenschaften **Aktualisieren** aus. Dadurch werden sowohl die Vorschau als auch der HTML-Codeausschnitt links auf der Seite aktualisiert, sodass das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können jederzeit **Zurücksetzen** auswählen, um alle Eigenschaften auf ihre Standardeinstellungen zurückzusetzen.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p108">After you configure any properties, choose **Update**. This updates both the preview and the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="c9b6c-144">Wählen Sie auf der linken Seite des Codeausschnittkatalogs unter **HTML-Code** die Option **In Zwischenablage kopieren** aus.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-144">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="c9b6c-145">Öffnen Sie im HTML-Editor das zugeordnete Netzlaufwerk auf dem Computer, und öffnen Sie dann die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, der bzw. dem Sie den Codeausschnitt hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-145">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to.</span></span>
    
  
11. <span data-ttu-id="c9b6c-146">Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-146">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="c9b6c-p109">Jeder Codeausschnitt enthält HTML-Code, der eine visuelle Vorschau der Komponente und der Beispieldaten zur Verfügung stellt. Diesen HTML-Code sollten Sie für die schreibgeschützte Vorschau innerhalb der Tags **<!--PS>** und **<!--PE>** nicht bearbeiten, da sich dieses Markup nur auf die Vorschau des Codeausschnitts zur Entwurfszeit auswirkt und nicht darauf, wie der Codeausschnitt auf der Livewebsite angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p109">Each snippet contains HTML that provides a visual preview of the component and sample data. You shouldn't modify this HTML for the read-only preview inside the **<!--PS>** and **<!--PE>** tags because this markup affects only the design-time preview of the snippet, not how the snippet will appear on the live site.</span></span>
    
  
12. <span data-ttu-id="c9b6c-149">Um die serverseitige Vorschau des Codeausschnitts anzuzeigen, speichern Sie die HTML-Datei, um die Änderungen mit der zugeordneten Datei ASP.NET zu synchronisieren. Aktualisieren Sie dann die serverseitige Vorschau im Entwurfs-Manager.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-149">To see the server-side preview of the snippet, save the HTML file to sync the changes to the associated ASP.NET file, and then refresh the server-side preview in Design Manager.</span></span>
    
    <span data-ttu-id="c9b6c-150">Anders als bei der Vorschau zur Entwurfszeit wird das Steuerelement in der serverseitigen Vorschau so angezeigt, wie es von SharePoint gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-150">Unlike the design-time preview, the server-side preview shows the control as rendered by SharePoint.</span></span>
    
  

## <a name="understand-the-markup-in-an-html-snippet"></a><span data-ttu-id="c9b6c-151">Überblick über das Markup eines HTML-Codeausschnitts</span><span class="sxs-lookup"><span data-stu-id="c9b6c-151">Understand the markup in an HTML snippet</span></span>
<span data-ttu-id="c9b6c-152"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="c9b6c-152"><a name="UnderstandMarkup"> </a></span></span>

<span data-ttu-id="c9b6c-153">Ein Codeausschnitt enthält vier Basisabschnitte:</span><span class="sxs-lookup"><span data-stu-id="c9b6c-153">A snippet contains four basic sections:</span></span>
  
    
    

- <span data-ttu-id="c9b6c-154">**Kopfzeile** mit Starttags **<div>** und **<!--CS>** (ausgenommen benutzerdefinierte ASP.NET-Codeausschnitte, die nicht in ein **<div>**-Tag verpackt sind)</span><span class="sxs-lookup"><span data-stu-id="c9b6c-154">**Header** with starting **<div>** and **<!--CS>** tags (except custom ASP.NET snippets, which are not wrapped in a **<div>** tag)</span></span>
    
  
- <span data-ttu-id="c9b6c-155">**SharePoint-Markup**, bei dem Codeausschnitte in **<!--MS>**-Starttags und **<!--ME>**-Endtags eingeschlossen sind</span><span class="sxs-lookup"><span data-stu-id="c9b6c-155">**SharePoint markup** where snippets are enclosed in **<!--MS>** start and **<!--ME>** end tags</span></span>
    
  
- <span data-ttu-id="c9b6c-156">**HTML-Vorschau** eingeschlossen in **<!--PS>**-Starttags und **<!--PE>**-Endtags</span><span class="sxs-lookup"><span data-stu-id="c9b6c-156">**HTML preview** enclosed in **<!--PS>** start and **<!--PE>** end tags</span></span>
    
  
- <span data-ttu-id="c9b6c-157">**Fußzeile** mit schließenden **<!--CE>**- und **</div>**-Tags</span><span class="sxs-lookup"><span data-stu-id="c9b6c-157">**Footer** with closing **<!--CE>** and **</div>** tags</span></span>
    
  
<span data-ttu-id="c9b6c-p110">Alle Abschnitte eines Codeausschnitts, mit Ausnahme der HTML-Vorschau, sind in HTML-Kommentare eingeschlossen, um Interaktionen mit dem Dokumentobjektmodell (Document Object Model, DOM) und vorhandenen Formatierungen zu vermeiden. Ein Codeausschnitt beginnt mit dem Namen einer Komponente und enthält dann das eigentliche ASP.NET-Markup, eine HTML-Vorschau zum Rendern zur Entwurfszeit sowie die Endtags. Das ASP.NET-Markup ist auskommentiert, doch SharePoint entfernt die Kommentartags und verwendet dieses Markup, wenn die HTML-Datei mit der MASTER-Datei oder der ASPX-Datei synchronisiert wird. Wenn Sie ASP.NET kennen, können Sie dieses Markup im Codeausschnitt anpassen.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p110">All sections of a snippet, except the HTML preview, are enclosed in HTML comments to avoid interactions with the Document Object Model (DOM) and existing styling. A snippet starts with the name of a component, and then includes its actual ASP.NET markup, an HTML preview for design-time rendering, and then ending tags. The ASP.NET markup is commented out, but SharePoint strips out the comment tags and uses this markup when the HTML file is synced to the .master or .aspx file. If you know ASP.NET, you can customize this markup in the snippet.</span></span>
  
    
    
<span data-ttu-id="c9b6c-162">Als Beispiel ist nachfolgend das Standardmarkup für einen Bearbeitungsmodusbereich darstellt. Dabei handelt es sich einfach um einen Container, der unter bestimmten Bedingungen andere Inhalte und Steuerelemente anzeigt.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-162">As an example, the following is the default markup for an Edit Mode Panel, which is simply a container that conditionally displays other content and controls.</span></span>
  
    
    

### <a name="header"></a><span data-ttu-id="c9b6c-163">Kopfzeile</span><span class="sxs-lookup"><span data-stu-id="c9b6c-163">Header</span></span>


```HTML

<div data-name="EditModePanelShowInEdit">
    <!--CS: Start Edit Mode Panel Snippet-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="c9b6c-164">SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-164">SharePoint markup</span></span>


```HTML

<!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
```


### <a name="html-preview"></a><span data-ttu-id="c9b6c-165">HTML-Vorschau</span><span class="sxs-lookup"><span data-stu-id="c9b6c-165">HTML preview</span></span>


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Edit Mode Panel Properties.
    
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="footer"></a><span data-ttu-id="c9b6c-166">Fußzeile</span><span class="sxs-lookup"><span data-stu-id="c9b6c-166">Footer</span></span>


```HTML

<!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Edit Mode Panel Snippet-->
</div>
```

<span data-ttu-id="c9b6c-167">Nachfolgend finden Sie das Standardmarkup für einen Codeausschnitt für die obere Navigationsleiste. Dies ist komplexer, da dieser Codeausschnitt verschiedene Steuerelemente enthält, von denen einige ineinander geschachtelt sind, einschließlich einer Datenquelle für die Navigationsausdrücke, einem Stellvertretungs-Steuerelement und einem Inhaltsplatzhalter.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-167">The following is the default markup for a Top Navigation snippet, which is more complex because this snippet contains several different controls, with some nested inside each other, including a data source for the navigation terms, a delegate control, and a content placeholder.</span></span>
  
> [!NOTE]
> <span data-ttu-id="c9b6c-168">Einige der Steuerelemente, wie beispielsweise der Inhaltsplatzhalter, enthalten leere Tags für eine HTML-Vorschau, da das Element keine visuelle Darstellung auf der Seite benötigt.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-168">Some of the controls, such as the content placeholder, contain empty tags for an HTML preview because that element does not require a visual representation on the page.</span></span> 
  
    
    


### <a name="header"></a><span data-ttu-id="c9b6c-169">Kopfzeile</span><span class="sxs-lookup"><span data-stu-id="c9b6c-169">Header</span></span>


```HTML

<div data-name="TopNavigationNoFlyoutWithStartNode">
<!--CS: Start Top Navigation Snippet-->    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" CssClass="edit-mode-panel">-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="c9b6c-170">SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-170">SharePoint markup</span></span>


```HTML

<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<SharePoint:AjaxDelta ID="DeltaTopNavigation" BlockElement="true" CssClass="ms-displayInline ms-core-navigation ms-dialogHidden" runat="server">-->
```


### <a name="html-preview"></a><span data-ttu-id="c9b6c-171">HTML-Vorschau</span><span class="sxs-lookup"><span data-stu-id="c9b6c-171">HTML preview</span></span>


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="c9b6c-172">SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-172">SharePoint markup</span></span>


```HTML

<!--MS:<SharePoint:DelegateControl runat="server" ControlId="TopNavigationDataSource" Id="topNavigationDelegate">-->
```


### <a name="html-preview"></a><span data-ttu-id="c9b6c-173">HTML-Vorschau</span><span class="sxs-lookup"><span data-stu-id="c9b6c-173">HTML preview</span></span>


```HTML
<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<span style="display:none">
<table cellpadding="4" cellspacing="0" style="font:messagebox;color:buttontext;background-color:buttonface;border: solid 1px;border-top-color:buttonhighlight;border-left-color:buttonhighlight;border-bottom-color:buttonshadow;border-right-color:buttonshadow">
<tr><td nowrap="nowrap">
<span style="font-weight:bold">PortalSiteMapDataSource</span> - topSiteMap</td></tr><tr><td></td></tr></table></span>
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="c9b6c-174">SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-174">SharePoint markup</span></span>


```HTML

<!--MS:<Template_Controls>-->
<!--MS:<asp:SiteMapDataSource ShowStartingNode="True" SiteMapProvider="SPNavigationProvider" ID="topSiteMap" runat="server" StartingNodeUrl="sid:1002">-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="c9b6c-175">SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-175">SharePoint markup</span></span>


```HTML

<!--ME:</asp:SiteMapDataSource>-->
<!--ME:</Template_Controls>-->
<!--ME:</SharePoint:DelegateControl>--><a name="startNavigation"></a>
```


### <a name="sharepoint-markup"></a><span data-ttu-id="c9b6c-176">SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-176">SharePoint markup</span></span>


```HTML

<!--MS:<asp:ContentPlaceHolder ID="PlaceHolderTopNavBar" runat="server">-->
<!--MS:<SharePoint:AspMenu ID="TopNavigationMenu" runat="server" EnableViewState="false" DataSourceID="topSiteMap" AccessKey="&amp;#60;%$Resources:wss,navigation_accesskey%&amp;#62;" UseSimpleRendering="true" UseSeparateCss="false" Orientation="Horizontal" StaticDisplayLevels="2" AdjustForShowStartingNode="false" MaximumDynamicDisplayLevels="0" SkipLinkText="">-->
```


### <a name="html-preview"></a><span data-ttu-id="c9b6c-177">HTML-Vorschau</span><span class="sxs-lookup"><span data-stu-id="c9b6c-177">HTML preview</span></span>


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<link rel="stylesheet" type="text/css" href="/_layouts/15/1033/styles/menu-21.css" />
<div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox">
<ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static">
<li class="static">
<a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" tabindex="0" title="Default Publishing Site" href="/sites/PubSite/Pages/default.aspx" accesskey="1">
<span class="additional-background ms-navedit-flyoutArrow">
<span class="menu-item-text">Default Publishing Site</span></span></a></li></ul></div>
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="c9b6c-178">SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-178">SharePoint markup</span></span>


```HTML

<!--ME:</SharePoint:AspMenu>-->
<!--ME:</asp:ContentPlaceHolder>-->
```


### <a name="html-preview"></a><span data-ttu-id="c9b6c-179">HTML-Vorschau</span><span class="sxs-lookup"><span data-stu-id="c9b6c-179">HTML preview</span></span>


```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)-->
<!--PE: End of READ-ONLY PREVIEW-->
```


### <a name="sharepoint-markup"></a><span data-ttu-id="c9b6c-180">SharePoint-Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-180">SharePoint markup</span></span>


```HTML

<!--ME:</SharePoint:AjaxDelta>-->
```


### <a name="footer"></a><span data-ttu-id="c9b6c-181">Fußzeile</span><span class="sxs-lookup"><span data-stu-id="c9b6c-181">Footer</span></span>


```HTML
<!--CE: End Top Navigation Snippet-->
</div>
```


### <a name="types-of-markup"></a><span data-ttu-id="c9b6c-182">Arten von Markup</span><span class="sxs-lookup"><span data-stu-id="c9b6c-182">Types of markup</span></span>

<span data-ttu-id="c9b6c-183">Es folgt eine Übersicht über die Arten von Markup, die in einem Codeausschnitt enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-183">Here is a breakdown of the types of markup that are included in a snippet.</span></span>
  
    
    
 <span data-ttu-id="c9b6c-184">**Registrierung eines SharePoint-Namespace** SPM ("SharePoint-Markup") gibt eine Zeile zur Registrierung eines SharePoint-Namespace an.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-184">**SharePoint namespace registration** SPM ("SharePoint markup") indicates a line registering a SharePoint namespace.</span></span>
  
    
    



```HTML

<!--SPM:<%@Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
```

 <span data-ttu-id="c9b6c-185">**Kommentare** CS und CE ("Kommentaranfang" und "Kommentarende") dienen zur Analyse der Markupzeilen.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-185">**Comments** CS and CE ("Comment start" and "comment end") help you parse the lines of markup.</span></span>
  
    
    



```HTML
<!--CS: Start Top Navigation Snippet-->
…
<!--CE: End Top Navigation Snippet-->

```

 <span data-ttu-id="c9b6c-p111">**Codeausschnitte** MS und ME ("Markupanfang" und "Markupende") bestimmen den Anfang und das Ende eines SharePoint-Steuerelements oder -Codeausschnitts. Einige Codeausschnitte, wie das Menüband oder das obige Steuerelement für die obere Navigationsleiste, enthalten verschiedene Steuerelemente, die in einem einzelnen Codeausschnitt geschachtelt sind.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p111">**Snippets** MS and ME ("markup start" and "markup end") denote the beginning and end of a SharePoint control or a snippet. Some snippets, like the ribbon or the Top Navigation control above, contain several controls nested within a single snippet.</span></span>
  
    
    



```HTML

<!--MS:<SharePoint:DelegateControl runat="server" ControlId="TopNavigationDataSource" Id="topNavigationDelegate">-->
…
<!--ME:</SharePoint:DelegateControl>--><a name="startNavigation"></a>

<!--MS:<Template_Controls>-->
…
<!--ME:</Template_Controls>-->

<!--MS:<asp:SiteMapDataSource ShowStartingNode="True" SiteMapProvider="SPNavigationProvider" ID="topSiteMap" runat="server" StartingNodeUrl="sid:1002">-->
…
<!--ME:</asp:SiteMapDataSource>-->

```

 <span data-ttu-id="c9b6c-p112">**Vorschaublöcke** PS und PE ("Vorschauanfang" und "Vorschauende") umgeben einen HTML-Codeabschnitt, den Sie nicht bearbeiten sollten. Diese Vorschauabschnitte sind eine Momentaufnahme des SharePoint-Steuerelements, das der Codeausschnitt einfügt. Mithilfe einer Vorschau können Sie in einem HTML-Editor auf Clientseite eine HTML-Datei besser bearbeiten. Doch das Ändern des Inhalts oder der Formatierung innerhalb dieser Vorschau hat keine bleibenden Auswirkungen auf die MASTER-Datei, die SharePoint letztlich nutzt. Zum Formatieren eines Codeausschnitts müssen Sie die SharePoint-Formate bestimmen und mit eigenen benutzerdefinierten CSS überschreiben.</span><span class="sxs-lookup"><span data-stu-id="c9b6c-p112">**Preview blocks** PS and PE ("Preview start" and "preview end") surround a section of HTML code that you should not edit. These preview sections are a snapshot in time of the SharePoint control that snippet is inserting. A preview makes it possible for you to work more meaningfully on the HTML file in a client-side HTML editor. But, changing the content or styling within that preview has no lasting effect on the .master file, which is what SharePoint is ultimately using. To style a snippet, you have to identify and override the SharePoint styles with your own custom CSS.</span></span>
  
    
    



```HTML

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><span style="display:none"><table cellpadding="4" cellspacing="0" style="font:messagebox;color:buttontext;background-color:buttonface;border: solid 1px;border-top-color:buttonhighlight;border-left-color:buttonhighlight;border-bottom-color:buttonshadow;border-right-color:buttonshadow"><tr><td nowrap="nowrap"><span style="font-weight:bold">PortalSiteMapDataSource</span> - topSiteMap</td></tr><tr><td></td></tr></table></span><!--PE: End of READ-ONLY PREVIEW-->

<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><link rel="stylesheet" type="text/css" href="/_layouts/15/1033/styles/menu-21.css" /><div id="zz7_TopNavigationMenu" class=" noindex ms-core-listMenu-horizontalBox"><ul id="zz9_RootAspMenu" class="root ms-core-listMenu-root static"><li class="static"><a class="static menu-item ms-core-listMenu-item ms-displayInline ms-navedit-linkNode" tabindex="0" title="Default Publishing Site" href="/sites/PubSite/Pages/default.aspx" accesskey="1"><span class="additional-background ms-navedit-flyoutArrow"><span class="menu-item-text">Default Publishing Site</span></span></a></li></ul></div><!--PE: End of READ-ONLY PREVIEW-->
```


## <a name="see-also"></a><span data-ttu-id="c9b6c-193">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="c9b6c-193">See also</span></span>
<span data-ttu-id="c9b6c-194"><a name="Resources"> </a></span><span class="sxs-lookup"><span data-stu-id="c9b6c-194"><a name="Resources"> </a></span></span>


-  [<span data-ttu-id="c9b6c-195">Vorgehensweise: Konvertieren einer HTML-Datei in eine Gestaltungsvorlage in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9b6c-195">How to: Convert an HTML file into a master page in SharePoint</span></span>](how-to-convert-an-html-file-into-a-master-page-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c9b6c-196">Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9b6c-196">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c9b6c-197">Vorgehensweise: hinzufügen einen Ausschnitt Bearbeiten Modus Systemsteuerung SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9b6c-197">How to: Add an Edit Mode Panel snippet in SharePoint</span></span>](how-to-add-an-edit-mode-panel-snippet-in-sharepoint.md)
    
  
-  [<span data-ttu-id="c9b6c-198">Vorgehensweise: Hinzufügen von Ausschnitt glätten Sicherheit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="c9b6c-198">How to: Add a Security Trim snippet in SharePoint</span></span>](how-to-add-a-security-trim-snippet-in-sharepoint.md)
    
  

