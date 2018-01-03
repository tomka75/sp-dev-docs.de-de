---
title: "Hinzufügen eines Bearbeitungsmodusbereichs-Codeausschnitts in SharePoint"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: 39fa1e32-9129-407d-914f-96f4c6e66dc8
ms.openlocfilehash: c5b971b72d8910ac511b27d96a441400afce5323
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="add-an-edit-mode-panel-snippet-in-sharepoint"></a><span data-ttu-id="3cac8-102">Hinzufügen eines Bearbeitungsmodusbereichs-Codeausschnitts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3cac8-102">How to: Add an Edit Mode Panel snippet in SharePoint</span></span>

<span data-ttu-id="3cac8-p101">Ein Bearbeitungsmodusbereich ist ein Codeausschnitt, den Sie verwenden können, um Anweisungen oder andere Inhalte für Inhaltsautoren anzuzeigen, die Inhalte dieses Bereichs nur sehen können, wenn sie eine Seite bearbeiten. Dieser Codeausschnitt kann hingegen auch so konfiguriert werden, dass seine Inhalte nur im regulären Modus (Ansichtsmodus) statt im Bearbeitungsmodus angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="3cac8-p101">An Edit Mode Panel is a snippet that you can use to display instructions or other content to content authors, who see the contents of that panel only when they edit a page. Conversely, this snippet can also be configured to display its contents only in regular (view) mode instead of in edit mode.</span></span>

## <a name="introduction-to-the-edit-mode-panel"></a><span data-ttu-id="3cac8-105">Einführung in die Bearbeitungsbereich Modus</span><span class="sxs-lookup"><span data-stu-id="3cac8-105">Introduction to the Edit Mode Panel</span></span>
<span data-ttu-id="3cac8-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="3cac8-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="3cac8-p102">Inhaltsautoren mit den erforderlichen Berechtigungen können in einer Veröffentlichungssite erstellen oder Bearbeiten von Seiten, die sich in der Bibliothek für Seiten befinden. In der Regel ein Autor erstellen oder Bearbeiten einer Seite auswählt und dann werden die verschiedenen Seitenfelder Inhalt hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="3cac8-p102">In a publishing site, content authors with the necessary permissions can create or edit pages that reside in the Pages library. Typically, an author chooses to create or edit a page, and then adds content to the various page fields.</span></span>
  
    
    
<span data-ttu-id="3cac8-p103">Wie ein Designer können Sie ein bearbeiten im Bereich zu einer Gestaltungsvorlage oder Seitenlayout hinzufügen, und den Inhalt der das Snippet werden für Inhaltsautoren sichtbar, nur, wenn sie entscheiden, basierend auf dieses Seitenlayout eine Seite oder eine Seite mit der Masterseite verknüpften bearbeiten. Ein bearbeiten im Bereich können Sie beispielsweise den folgenden Inhalt nur für Inhaltsautoren anzuzeigen, wenn die Seite im Bearbeitungsmodus befindet:</span><span class="sxs-lookup"><span data-stu-id="3cac8-p103">As a designer, you can add an Edit Mode Panel to a master page or page layout, and the contents of that snippet will be visible to content authors only when they choose to edit a page based on that page layout or a page associated with that master page. For example, you can use an Edit Mode Panel to display the following content only to content authors when the page is in edit mode:</span></span>
  
    
    

- <span data-ttu-id="3cac8-111">Ein Page-Feld, wie etwa **Schedule Publishing Date**, dies ist wichtig, zu der Inhaltsautor, jedoch nicht für Besucher die Seite auf der online geschalteten Website anzeigen.</span><span class="sxs-lookup"><span data-stu-id="3cac8-111">A page field, such as **Schedule Publishing Date**, that's important to the content author but not to visitors viewing the page on the live site.</span></span>
    
  
- <span data-ttu-id="3cac8-112">Eine Beschreibung des welche Art von Inhalt in einem Feld eingegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="3cac8-112">A description of what kind of content should be entered in a page field.</span></span>
    
  
- <span data-ttu-id="3cac8-113">Ein Hinweis für Autoren von Inhalten, die sie berücksichtigen sollten, wie die Seite für verschiedenen Gerätekanälen aussieht.</span><span class="sxs-lookup"><span data-stu-id="3cac8-113">A note to content authors that they should consider how the page looks for different device channels.</span></span>
    
  
<span data-ttu-id="3cac8-114">Sie können auch Links zu anderen Stylesheets in einer bearbeiten im Bereich ablegen, damit Sie verschiedene Formate für den Bearbeitungsmodus im Vergleich zu Ansichtsmodus bereitstellen können.</span><span class="sxs-lookup"><span data-stu-id="3cac8-114">You can also put links to different style sheets in an Edit Mode Panel so that you can provide different styling for edit mode vs. view mode.</span></span>
  
    
    
<span data-ttu-id="3cac8-p104">Sie sollten im Modus bearbeiten, einem Seitenlayout hinzufügen, wenn die Notizen für Autoren von Inhalten für den Inhaltstyp spezifisch sind auf dem dieses Seitenlayout basiert. Sie können auch dieser Ausschnitt in eine Gestaltungsvorlage hinzufügen, wenn die Notizen für Autoren, die alle Seiten gelten, die der Masterseite zugeordnet werden, z. B., ob die Systemsteuerung Anweisungen für die Angabe von Inhalt für ein bestimmtes Gerätekanal enthalten ist, verwendet die Masterseite.</span><span class="sxs-lookup"><span data-stu-id="3cac8-p104">You should add the Edit Mode Panel to a page layout when the notes for content authors are specific to the content type on which that page layout is based. You can also add this snippet to a master page when the notes for authors are applicable to all pages that will be associated with that master page—for example, if the panel will contain instructions for supplying content for a specific device channel that uses that master page.</span></span>
  
    
    
<span data-ttu-id="3cac8-117">Sie können auch ein bearbeiten im Bereich zum Anzeigen des Inhalts nur im regulären Modus, anstatt Bearbeitungsmodus festlegen, wenn Sie ein Szenario haben, in dem es ist hilfreich oder hilfreiche Inhalte nur für Besucher der Website anzeigen (jedoch nicht content-Autoren) Wenn sie eine Seite bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="3cac8-117">You can also set an Edit Mode Panel to display its contents only in regular mode, instead of edit mode, if you have a scenario where it's useful or helpful to display content only to site visitors (but not content authors) when they're editing a page.</span></span>
  
    
    

### <a name="insert-an-edit-mode-panel"></a><span data-ttu-id="3cac8-118">Einfügen eines bearbeiten im Bereichs</span><span class="sxs-lookup"><span data-stu-id="3cac8-118">Insert an Edit Mode Panel</span></span>
<span data-ttu-id="3cac8-119"><a name="InsertSnippet"> </a></span><span class="sxs-lookup"><span data-stu-id="3cac8-119"><a name="InsertSnippet"> </a></span></span>

<span data-ttu-id="3cac8-p105">Wie alle Ausschnitte fügen Sie dieser Ausschnitt aus Codeausschnittkatalog. Zum Codeausschnittkatalog zu navigieren, müssen Sie zuerst eine Gestaltungsvorlage oder Seitenlayout bearbeiten auswählen.</span><span class="sxs-lookup"><span data-stu-id="3cac8-p105">Like all snippets, you add this snippet from the Snippet Gallery. To navigate to the Snippet Gallery, you must first select a master page or page layout to edit.</span></span>
  
    
    

### <a name="to-insert-an-edit-mode-panel"></a><span data-ttu-id="3cac8-122">So fügen Sie einen Bereich Bearbeitungsmodus ein</span><span class="sxs-lookup"><span data-stu-id="3cac8-122">To insert an Edit Mode panel</span></span>


1. <span data-ttu-id="3cac8-123">Wechseln Sie zu Ihrer Veröffentlichungswebsite.</span><span class="sxs-lookup"><span data-stu-id="3cac8-123">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="3cac8-124">Wählen Sie in der rechten oberen Ecke der Seite das Zahnradsymbol für Einstellungen und dann **Entwurfs-Manager** aus.</span><span class="sxs-lookup"><span data-stu-id="3cac8-124">In the upper-right corner of the page, choose the Settings gear, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="3cac8-125">Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Gestaltungsvorlagen bearbeiten** oder **Seitenlayouts bearbeiten** aus, je nachdem, welchen Dateityp Sie bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="3cac8-125">In Design Manager, in the left navigation pane, choose **Edit Master Pages** or **Edit Page Layouts**, depending on what type of file you're editing.</span></span>
    
  
4. <span data-ttu-id="3cac8-126">Wählen Sie den Namen der Masterseite oder Seitenlayout, das Sie den Codeausschnitt hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="3cac8-126">Select the name of the master page or page layout that you want to add the snippet to.</span></span>
    
  
5. <span data-ttu-id="3cac8-127">Wählen Sie zum Öffnen des Codeausschnittkatalogs in der serverseitigen Vorschau in der rechten oberen Ecke **Codeausschnitte** aus.</span><span class="sxs-lookup"><span data-stu-id="3cac8-127">To open the Snippet Gallery, choose **Snippets** in the upper-right corner of the server-side preview.</span></span>
    
  
6. <span data-ttu-id="3cac8-128">Klicken Sie im Menüband auf der Registerkarte **Entwurf** wählen Sie **Im Bereich bearbeiten**, und wählen Sie dann den Modus, in dem Sie Ihre Ausschnitt angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="3cac8-128">On the ribbon, on the **Design** tab, choose **Edit Mode Panel**, and then choose the mode that you want your snippet to be displayed in.</span></span>
    
  
7. <span data-ttu-id="3cac8-129">Im Codeausschnittkatalog können auf der rechten Seite auf **Infos zu dieser Komponente** klicken oder diese Option auswählen, um Eigenschaftengruppen ein- oder auszublenden, und anschließend die gewünschten benutzerdefinierten Einstellungen konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="3cac8-129">On the right side of the Snippet Gallery, under **About this Component**, click or select section headers to expand or collapse groups of properties, and then configure any custom settings that you want.</span></span>
    
    <span data-ttu-id="3cac8-p106">Im Abschnitt mit dem Namen wichtig enthält die Eigenschaften, die angezeigt werden, die Funktionsweise dieser bestimmten Ausschnitts wichtig sind. Für einen Bereich bearbeiten Modus wird die **PageDisplayMode** -Eigenschaft festgelegt werden, **Edit** oder **Display**, je nach den Modus an, dem Sie auf dem Menüband ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="3cac8-p106">The section named Important contains the properties that are most important to how this particular snippet works. For an Edit Mode Panel, the **PageDisplayMode** property will be set to either **Edit** or **Display**, depending on the mode that you selected on the ribbon.</span></span>
    
  
8. <span data-ttu-id="3cac8-p107">Nachdem Sie Eigenschaften konfiguriert haben, wählen Sie **Aktualisieren**. Dadurch wird der HTML-Codeausschnitt links auf der Seite aktualisiert, sodass das Markup Ihre benutzerdefinierten Einstellungen widerspiegelt. Sie können stets **Zurücksetzen** wählen, um alle Eigenschaften auf ihre Standardeinstellungen zurückzusetzen.</span><span class="sxs-lookup"><span data-stu-id="3cac8-p107">After you configure any properties, choose **Update**. This updates the HTML snippet on the left side of the page, so that the markup reflects your custom settings. You can always choose **Reset** to return all properties to their default settings.</span></span>
    
  
9. <span data-ttu-id="3cac8-135">Wählen Sie links im Codeausschnittkatalog unter **HTML-Codeausschnitt** den Befehl **In Zwischenablage kopieren**.</span><span class="sxs-lookup"><span data-stu-id="3cac8-135">On the left side of the Snippet Gallery, under **HTML Snippet**, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="3cac8-p108">Öffnen Sie in der HTML-Editor das zugeordnete Netzlaufwerk, auf dem Computer, und öffnen Sie die HTML-Datei für die Gestaltungsvorlage oder das Seitenlayout, das Sie den Codeausschnitt hinzufügen möchten. Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="3cac8-p108">In your HTML editor, open the mapped network drive on your computer, and then open the HTML file for the master page or page layout that you're adding the snippet to. For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span>
    
  
11. <span data-ttu-id="3cac8-138">Fügen Sie den Codeausschnitt in der HTML-Datei an der Stelle ein, an der das Markup angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="3cac8-138">In the HTML file, paste the snippet where you want the markup to appear.</span></span>
    
    <span data-ttu-id="3cac8-p109">Wenn Sie im Modus bearbeiten, einem Seitenlayout hinzufügen, stellen Sie sicher, dass Sie den Codeausschnitt innerhalb des **PlaceHolderMain** einzufügen, sodass der Bereich Inhaltsautoren im Bearbeitungsmodus sichtbar ist. Können Sie den Codeausschnitt unmittelbar vor einem bestimmten Feld einfügen, oder Sie können eine oder mehrere Seitenfelder innerhalb des Bereichs der Bearbeiten Modus versetzen.</span><span class="sxs-lookup"><span data-stu-id="3cac8-p109">If you're adding the Edit Mode Panel to a page layout, make sure to paste the snippet inside **PlaceHolderMain** so that the panel is visible to content authors in edit mode. You can paste the snippet immediately before a specific page field, or you can put one or more page fields inside the Edit Mode Panel.</span></span>
    
  
12. <span data-ttu-id="3cac8-141">Ersetzen Sie die **<div>**, in dem `class="DefaultContentBlock"` mit Ihren eigenen spezifischen Inhalt - beispielsweise mit Anmerkungen oder Anweisungen, um Inhaltsautoren oder bestimmte Seitenfelder, die für Autoren, aber nicht Besucher der Website hilfreich sind.</span><span class="sxs-lookup"><span data-stu-id="3cac8-141">Replace the **<div>** where `class="DefaultContentBlock"` with your own specific content—for example, with notes or instructions to content authors, or specific page fields that are useful for authors but not site visitors.</span></span>
    
  
13. <span data-ttu-id="3cac8-142">Speichern Sie die Seite, und aktualisieren Sie die serverseitige Vorschau im Entwurfs-Manager, um sicherzustellen, dass im Modus bearbeiten wie gewünscht angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="3cac8-142">Save the page, and then refresh the server-side preview in Design Manager to make sure the Edit Mode Panel appears as expected.</span></span>
    
  

## <a name="understand-the-snippet-markup"></a><span data-ttu-id="3cac8-143">Grundlegendes zu codeausschnittmarkup</span><span class="sxs-lookup"><span data-stu-id="3cac8-143">Understand the snippet markup</span></span>
<span data-ttu-id="3cac8-144"><a name="UnderstandMarkup"> </a></span><span class="sxs-lookup"><span data-stu-id="3cac8-144"><a name="UnderstandMarkup"> </a></span></span>

<span data-ttu-id="3cac8-p110">Die beiden wichtigsten Teile eines Ausschnitts bearbeiten im Bereich der **PageDisplayMode** -Eigenschaft und die **<div>** sind, in dem `class="DefaultContentBlock"`. Die **PageDisplayMode** -Eigenschaft bestimmt, ob der Inhalt des Bereichs angezeigt werden, nur im Bearbeitungsmodus oder reguläre/Anzeigemodus (d. h., wenn die Seite nicht im Bearbeitungsmodus befindet).</span><span class="sxs-lookup"><span data-stu-id="3cac8-p110">The two most important parts of an Edit Mode Panel snippet are the **PageDisplayMode** property and the **<div>** where `class="DefaultContentBlock"`. The **PageDisplayMode** property determines whether the contents of the panel are displayed only in edit mode or in regular/display mode (meaning whenever the page is not in edit mode).</span></span>
  
> [!NOTE]
> <span data-ttu-id="3cac8-147">Diese Eigenschaft wird nicht im Markup angezeigt, es sei denn, Sie ändern den Wert in **Display**.</span><span class="sxs-lookup"><span data-stu-id="3cac8-147">Note: This property doesn't appear in the markup unless you change the value to **Display**.</span></span> <span data-ttu-id="3cac8-148">Wenn die Eigenschaft nicht im Markup angezeigt wird, ist der Standardmodus für den Ausschnitt der Bearbeitungsmodus.</span><span class="sxs-lookup"><span data-stu-id="3cac8-148">When the property does not appear in the markup, the default mode for the snippet is Edit mode.</span></span> 
  
    
    

<span data-ttu-id="3cac8-149">Die **<div>**, wobei `class="DefaultContentBlock"` ist, was Sie mit Ihren eigenen Inhalt ersetzen die anderen Snippets und Steuerelemente enthalten können.</span><span class="sxs-lookup"><span data-stu-id="3cac8-149">The **<div>** where `class="DefaultContentBlock"` is what you replace with your own content, which can include other snippets and controls.</span></span>
  
    
    



```HTML

<div data-name="EditModePanelShowInEdit">
    <!--CS: Start Edit Mode Panel Snippet-->
    <!--SPM:<%@Register Tagprefix="Publishing" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
    <!--MS:<Publishing:EditModePanel runat="server" PageDisplayMode="Display" CssClass="edit-mode-panel">-->
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
        <div class="DefaultContentBlock" style="border:medium black solid; background:yellow; color:black; margin:20px; padding:10px;">
        You should replace this div with content that renders based on your Edit Mode Panel Properties.
        </div>
        <!--PS: Start of READ-ONLY PREVIEW (do not modify)--><!--PE: End of READ-ONLY PREVIEW-->
    <!--ME:</Publishing:EditModePanel>-->
    <!--CE: End Edit Mode Panel Snippet-->
</div>
```


## <a name="see-also"></a><span data-ttu-id="3cac8-150">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3cac8-150">See also</span></span>
<span data-ttu-id="3cac8-151"><a name="AdditionalResources"> </a></span><span class="sxs-lookup"><span data-stu-id="3cac8-151"><a name="AdditionalResources"> </a></span></span>


-  [<span data-ttu-id="3cac8-152">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="3cac8-152">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  
-  [<span data-ttu-id="3cac8-153">Vorgehensweise: Hinzufügen von Ausschnitt glätten Sicherheit in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3cac8-153">How to: Add a Security Trim snippet in SharePoint</span></span>](how-to-add-a-security-trim-snippet-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3cac8-154">Erstellen von Websites für SharePoint</span><span class="sxs-lookup"><span data-stu-id="3cac8-154">Build sites for SharePoint</span></span>](build-sites-for-sharepoint.md)
    
  
-  [<span data-ttu-id="3cac8-155">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3cac8-155">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  

