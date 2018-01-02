---
title: Anwenden von Formatvorlagen auf Seitenfelder in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: e227613d-0e4d-4312-924d-bb55e1fe4293
ms.openlocfilehash: 70cc908d0175bb2719e7dac73edaed3aacdea4ed
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="apply-styles-to-page-fields-in-sharepoint"></a><span data-ttu-id="3f4ae-102">Anwenden von Formatvorlagen auf Seitenfelder in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3f4ae-102">How to: Apply styles to page fields in SharePoint</span></span>
<span data-ttu-id="3f4ae-p101">In einem Seitenlayout können Sie Formate auf ein Seitenfeld anwenden. Diese Formate werden dann auf alle Inhalte angewendet, die von Inhaltsautoren hinzugefügt werden, wenn sie eine Seite mithilfe dieses Seitenlayouts erstellen. Darüber hinaus stehen Ihnen weitere Optionen zur Verfügung, mit denen Sie steuern können, wie Inhalte in einem RichHtmlField-Seitenfeld formatiert werden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p101">In a page layout, you can apply styles to a page field, and those styles are applied to any content added by content authors when they create a page from that page layout. Also, you have further options to control how content in a RichHtmlField page field is styled.</span></span>
## <a name="introduction-to-applying-styles-to-page-fields"></a><span data-ttu-id="3f4ae-105">Einführung in das Anwenden von Formatvorlagen für Seitenfelder</span><span class="sxs-lookup"><span data-stu-id="3f4ae-105">Introduction to applying styles to page fields</span></span>
<span data-ttu-id="3f4ae-106"><a name="Introduction"> </a></span><span class="sxs-lookup"><span data-stu-id="3f4ae-106"><a name="Introduction"> </a></span></span>

<span data-ttu-id="3f4ae-p102">Als Designer benötigen Sie die ultimative Kontrolle über die Positionierung und Formatierung von Seitenfeldern in einem Seitenlayout und auf allen Seiten, die mit diesem Seitenlayout erstellt wurden. Wenn Inhaltsautoren Seiten von einem Browser erstellen, können sie Seitenfelder auf der Seite nicht verschieben oder die von Ihnen angegebenen Formatvorlagen überschreiben. So wird sichergestellt, dass Ihr Branding über alle Seiten der Website konsistent bleibt.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p102">As a designer, you have ultimate control over the positioning and styling of page fields on a page layout and on any pages created from that page layout. When content authors create pages from a browser, they can't move page fields on the page or override the styles that you specify. This helps to ensure that your branding remains consistent through all pages in the site.</span></span>
  
    
    
<span data-ttu-id="3f4ae-110">Wenn Sie Formatvorlagen auf Seitenfelder anwenden, gibt es zwei grundlegende Kategorien von Feldtypen, die berücksichtigt werden müssen:</span><span class="sxs-lookup"><span data-stu-id="3f4ae-110">When you apply styles to page fields, there are two basic categories of field types to consider:</span></span>
  
    
    

- <span data-ttu-id="3f4ae-p103">**Andere Feldtypen als RichHtmlField** Die Seitenfelder, aus denen ein Seitenlayout besteht, entsprechen dem Inhaltstyp für dieses Seitenlayout. Ein Seitenfeld kann vielen Typen entsprechen, z. B. einer einzelnen Textzeile (TextField) oder mehreren Textzeilen (NoteField). Als Designer können Sie Formatvorlagen für alle diese Seitenfelder auf dieselbe Weise anwenden, indem Sie Formatvorlagen direkt auf das Seitenfeld im Seitenlayout anwenden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p103">**Field types other than RichHtmlField** The page fields that make up a page layout conform to the content type for that page layout. A page field can be of many types, such as a Single Line of Text (TextField) or Multiple Lines of Text (NoteField). As a designer, you can apply styles to all of these page fields in the same way, by applying styles to the page field directly on the page layout.</span></span>
    
  
- <span data-ttu-id="3f4ae-p104">**RichHtmlField** Das Rich-HTML-Feldsteuerelement (das auch als Publishing-HTML-Feld bezeichnet wird) ist eins der leistungsstärksten und am häufigsten verwendete Steuerelemente in Seitenlayouts. Standardmäßig verwenden Inhaltsautoren in einem Rich-HTML-Feld das Menüband zum Formatieren und Anwenden von Formatvorlagen auf Inhalte sowie zum Einfügen von Tabellen, Medien wie Bilder und Videos sowie Webparts. Dieser Feldtyp ist hilfreich, wenn Sie Inhaltsautoren die Freiheit geben möchten, Inhalte innerhalb der Parameter hinzuzufügen und zu formatieren, die Sie steuern können. Sie können ein RichHtmlField auf zwei Arten steuern:</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p104">**RichHtmlField** The rich HTML field control (also known as a Publishing HTML field) is one of the most powerful and frequently used controls in page layouts. By default, in a rich HTML field, content authors use the ribbon to format and apply styles to content, and to insert tables, media such as images and video, and Web Parts. This field type is useful when you want to give content authors the freedom to add and style content within parameters that you can control. You can control a RichHtmlField in two ways:</span></span>
    
  - <span data-ttu-id="3f4ae-p105">**Erstellen eines benutzerdefinierten Stylesheets** Standardmäßig stammen die Formatvorlagen, die auf dem Menüband eines RichHtmlField verfügbar sind, aus einem Stylesheet namens HtmlEditorStyles.css. Sie können die Eigenschaft **PrefixStyleSheet** für diesen Codeausschnitt konfigurieren, damit auf dem Menüband Ihre eigenen benutzerdefinierten Formatvorlagen für Inhaltsautoren angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p105">**Create a custom style sheet** By default, the styles available on the ribbon of a RichHtmlField come from a style sheet named HtmlEditorStyles.css. You can configure the **PrefixStyleSheet** property for this snippet so that your own custom styles appear on the ribbon for content authors to use.</span></span>
    
  
  - <span data-ttu-id="3f4ae-p106">**Konfigurieren der Allow-Eigenschaften** Ein Codeausschnitt für ein RichHtmlField hat 28 verfügbare Eigenschaften, die mit **Allow** beginnen, und Sie können diese Eigenschaften verwenden, um bestimmte Befehle oder Gruppen von Befehlen auf dem Menüband nicht für Inhaltsautoren verfügbar zu machen. Wenn Sie z. B. die Eigenschaft **AllowFontsMenu** auf **False** festlegen, können Autoren Schriftartmenü auf dem Menüband nicht verwenden, um zu ändern, welche Schriftart auf Text angewendet wird. Stattdessen können sie nur die von Ihnen angegebenen CSS-Formatvorlagen verwenden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p106">**Configure the Allow properties** A snippet for a RichHtmlField has 28 available properties that start with **Allow**, and you can use these properties to make specific commands or groups of commands on the ribbon unavailable to content authors. For example, if you set the **AllowFontsMenu** property to **False**, authors cannot use the Font menu on the ribbon to change what font is applied to text; instead, they can use only the CSS styles that you specify.</span></span>
    
  
<span data-ttu-id="3f4ae-p107">Für alle Arten von Seitenfeldern, einschließlich RichHtmlField, bestimmt der Designer, wie der Inhalt formatiert wird. Sie können RichHtmlField verwenden, um Inhaltsautoren die Freiheit zu geben, attraktive Inhalte einzufügen und Formatvorlagen anzuwenden. Sie behalten dennoch die ultimative Kontrolle darüber, welche Inhalte hinzugefügt und welche Formatvorlagen angewendet werden können.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p107">For all types of page fields, including the RichHtmlField, the designer determines how the content is styled. You can use the RichHtmlField to give content authors the freedom to insert rich content and apply styles; you still have ultimate control over what content can be added and what styles can be applied.</span></span>
  
    
    

## <a name="applying-styles-to-page-fields-other-than-richhtmlfield"></a><span data-ttu-id="3f4ae-124">Anwenden von Formatvorlagen auf andere Seitenfelder als RichHtmlField</span><span class="sxs-lookup"><span data-stu-id="3f4ae-124">Applying styles to page fields other than RichHtmlField</span></span>
<span data-ttu-id="3f4ae-125"><a name="Applying"> </a></span><span class="sxs-lookup"><span data-stu-id="3f4ae-125"><a name="Applying"> </a></span></span>

<span data-ttu-id="3f4ae-p108">Mit einem Seitenfeld-Steuerelement definieren Sie die Formate des Inhalts. Autoren können einer Seite Inhalte hinzufügen, doch der Designer steuert, wie diese Inhalte mittels CSS gerendert werden, die auf diese Steuerelemente angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p108">With a page field control, you can define the styles used by the content. Authors can add content to a page, but the designer controls how that content is rendered through CSS applied to those controls.</span></span>
  
    
    
<span data-ttu-id="3f4ae-128">Im HTML-Seitenlayout ist jedes Seitenfeld von einem**\<div\>**-Tag umschlossen.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-128">In the HTML page layout, each page field is wrapped in a **\<div\>** tag.</span></span> <span data-ttu-id="3f4ae-129">Um eine Formatvorlage auf ein Seitenfeld anzuwenden, können Sie einfach eine Formatvorlage auf **\<div\>** anwenden, z. B. `<div style="font-weight:bold"`.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-129">To apply a style to a page field, you can simply add a style to the **\<div\>**—for example,  `<div style="font-weight:bold"`.</span></span> <span data-ttu-id="3f4ae-130">Das häufigere und praktischere Szenario besteht jedoch darin, dass Sie ein **ID**-Attribut zu **\<div\>** für jedes Seitenfeld im Seitenlayout hinzufügen und dann die **ID** als Selektor für Formatvorlagen verwenden, die sich in einer externen Formatvorlage befinden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-130">But the more common and useful scenario is that you add an **id** attribute to the **\<div\>** for each page field in the page layout, and then use the **id** as a selector for styles that reside in an external style sheet.</span></span> <span data-ttu-id="3f4ae-131">Wenn Sie über mehrere Gerätekanäle verfügen und jeder Kanal seine eigene Formatvorlage aufweist, können Sie so unterschiedliche Formatvorlagen auf jedes Seitenfeld für jeden Kanal anwenden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-131">This way, if you have multiple device channels, and each channel has its own style sheet, you can apply different styles to each page field for each channel.</span></span> <span data-ttu-id="3f4ae-132">Das folgende Seitenfeld des Typs „TextField“ (auch als mehrere Textzeilen bezeichnet) weist möglicherweise nur ein **ID**-Attribut im **\<div\>**-Tag auf.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-132">For example, the following page field of the type TextField (also called Multiple Lines of Text) might have only an **id** attribute on the **\<div\>** tag.</span></span>
  
    
    



```HTML

<div id="ShortSummaryPageField">
<!--CS: Start Page Field: ShortSummary Snippet-->
<!--SPM:<%@Register Tagprefix="PageFieldNoteField" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<PageFieldNoteField:NoteField FieldName="a5249942-2dc5-4917-85e2-661d019ad548" runat="server">-->
<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><div align="left" class="ms-formfieldcontainer"><div class="ms-formfieldlabelcontainer" nowrap="nowrap"><span class="ms-formfieldlabel" nowrap="nowrap">ShortSummary</span></div><div class="ms-formfieldvaluecontainer"><div class="ms-rtestate-field">ShortSummary field value.</div></div></div><!--PE: End of READ-ONLY PREVIEW-->
<!--ME:</PageFieldNoteField:NoteField>-->
<!--CE: End Page Field: ShortSummary Snippet-->
</div>
```

<span data-ttu-id="3f4ae-133">Weitere Informationen dazu, wo Formatvorlagen und Formatvorlagenverweise für ein Seitenlayout eingefügt werden sollen, finden Sie unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3f4ae-133">For more information about where styles and style references for a page layout should go, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
  
    
    

## <a name="disabling-options-on-the-ribbon-of-a-richhtmlfield"></a><span data-ttu-id="3f4ae-134">Deaktivieren von Optionen auf dem Menüband eines RichHtmlField</span><span class="sxs-lookup"><span data-stu-id="3f4ae-134">Disabling options on the ribbon of a RichHtmlField</span></span>
<span data-ttu-id="3f4ae-135"><a name="Disabling"> </a></span><span class="sxs-lookup"><span data-stu-id="3f4ae-135"><a name="Disabling"> </a></span></span>

<span data-ttu-id="3f4ae-136">Wenn Inhaltsautoren eine Seite erstellen oder bearbeiten und dann Inhalt zu einem RichHtmlField mit einem Browser hinzufügen, können sie die Befehle auf dem Menüband für dieses Feld verwenden, um es zu formatieren, eine Formatvorlage anzuwenden oder attraktive Inhalte und Medien hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-136">When content authors create or edit a page and then add content to a RichHtmlField using a browser, they can use commands on the ribbon for that field to format, style, or insert rich content and media.</span></span> 
  
    
    
<span data-ttu-id="3f4ae-p110">Im Codeausschnittkatalog können Sie die Eigenschaften für ein Seitenfeld vom Typ RichHtmlField so konfigurieren, dass bestimmte Befehle oder Gruppen von Befehlen auf dem Menüband nicht für Autoren verfügbar sind. Wenn Sie z. B. die Eigenschaft **AllowFontSizesMenu** auf **False** festlegen, können Sie die **Font Size**-Gruppe auf dem Menüband deaktivieren. Durch Festlegen der Eigenschaft **AllowFonts** auf **False** können Sie die gesamte Gruppe **Schriftart** auf dem Menüband deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p110">In the Snippet Gallery, you can configure the properties of a page field of the type RichHtmlField, so that specific commands or groups of commands on the ribbon are made unavailable to authors. For example, by setting the **AllowFontSizesMenu** property to **False**, you can disable the **Font Size** menu on the ribbon. By setting the **AllowFonts** property to **False**, you can disable the entire **Font** group on the ribbon.</span></span>
  
    
    
<span data-ttu-id="3f4ae-140">Wenn Sie diese Eigenschaften im Codeausschnittkatalog konfiguriert haben und dann den Codeausschnitt aktualisieren, werden die Eigenschaften im Codeausschnittmarkup innerhalb des  `<!--MS:>`-Kommentars angezeigt.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-140">After you configure these properties in the Snippet Gallery and then update the snippet, the properties appear in the snippet markup inside the  `<!--MS:>` comment.</span></span>
  
    
    



```HTML

<div data-name="Page Field: ArticleBody">
<!--CS: Start Page Field: ArticleBody Snippet-->
<!--SPM:<%@Register Tagprefix="PageFieldRichHtmlField" Namespace="Microsoft.SharePoint.Publishing.WebControls" Assembly="Microsoft.SharePoint.Publishing, Version=15.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"%>-->
<!--MS:<PageFieldRichHtmlField:RichHtmlField runat="server" AllowFonts="False" FieldName="db3168db-8778-4fb6-a48f-57f598497388">-->
<!--PS: Start of READ-ONLY PREVIEW (do not modify)--><div id="ctl02_label" style="display:none">ArticleBody</div><div id="ctl02__ControlWrapper_RichHtmlField" class="ms-rtestate-field" style="display:inline" aria-labelledby="ctl02_label"><div align="left" class="ms-formfieldcontainer"><div class="ms-formfieldlabelcontainer" nowrap="nowrap"><span class="ms-formfieldlabel" nowrap="nowrap">ArticleBody</span></div><div class="ms-formfieldvaluecontainer"><div class="ms-rtestate-field">ArticleBody field value. Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</div></div></div></div>
<!--PE: End of READ-ONLY PREVIEW-->
<!--ME:</PageFieldRichHtmlField:RichHtmlField>-->
<!--CE: End Page Field: ArticleBody Snippet-->
</div>
```

> [!NOTE]
> <span data-ttu-id="3f4ae-141">Wenn Sie **AllowFonts** auf **False** festlegen, können Autoren von Inhalten weiterhin Tastenkombinationen wie STRG+B (fett) verwenden, um Text zu formatieren.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-141">Note: If you set **AllowFonts** to **False**, content authors can still use keyboard shortcuts such as CTRL+B (strong) to format text.</span></span> <span data-ttu-id="3f4ae-142">Um zu verhindern, dass Autoren Formatvorlagen zu Text hinzufügen, können Sie **AllowTextMarkup** auf **False** festlegen.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-142">To prevent authors from adding any styles to text, you can set **AllowTextMarkup** to **False**.</span></span> <span data-ttu-id="3f4ae-143">Bei dieser Einstellung gibt der HTML-Editor im Browser einen Fehler zurück, wenn Autoren von Inhalten versuchen, Inhalte zu speichern, die Formatvorlagen enthalten, die auf Text angewendet wurden. Außerdem wird der Autor aufgefordert, das ungültige Markup zu entfernen.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-143">With this setting, when content authors attempt to save content that contains styles applied to text, the HTML editor in the browser returns an error and prompts the author to remove the markup that is not valid.</span></span> 
  
    
    

<span data-ttu-id="3f4ae-p112">Ein RichHtmlField-Seitenfeld enthält 28 verschiedene **Allow**-Eigenschaften. Weitere Informationen dazu, was die jeweiligen Eigenschaften steuern, finden Sie unter  [RichHtmlField-Eigenschaften](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.publishing.webcontrols.richhtmlfield_properties) Weitere Informationen zum Hinzufügen und Konfigurieren von Codeausschnitten finden Sie unter [Codeausschnitte des SharePoint-Entwurfs-Managers](sharepoint-design-manager-snippets.md).</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p112">A RichHtmlField page field contains 28 different **Allow** properties. For more information about what specific properties control, see [RichHtmlField properties](http://msdn.microsoft.com/de-DE/library/microsoft.sharepoint.publishing.webcontrols.richhtmlfield_properties) For more information about adding and configuring snippets, see [SharePoint Design Manager snippets](sharepoint-design-manager-snippets.md).</span></span>
  
    
    

## <a name="controlling-the-styles-available-in-a-richhtmlfield"></a><span data-ttu-id="3f4ae-146">Steuern der in einem RichHtmlField verfügbaren Formatvorlagen</span><span class="sxs-lookup"><span data-stu-id="3f4ae-146">Controlling the styles available in a RichHtmlField</span></span>
<span data-ttu-id="3f4ae-147"><a name="Controlling"> </a></span><span class="sxs-lookup"><span data-stu-id="3f4ae-147"><a name="Controlling"> </a></span></span>

<span data-ttu-id="3f4ae-p113">In einem RichHtmlField können Inhaltsautoren Optionen auf dem Menüband verwenden, um Inhalte zu formatieren. Diese Formatierungsoptionen werden mithilfe von CSS implementiert, und diese Formatvorlagen sind in einem SharePoint-Stylesheet namens HtmlEditorStyles.css definiert, das sich auf dem Server an einem der folgenden Speicherorte befindet:</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p113">In a RichHtmlField, content authors can use options on the ribbon to format content. These formatting options are implemented by using CSS, and these styles are defined in a SharePoint style sheet named HtmlEditorStyles.css that resides on the server at one of the following locations:</span></span>
  
    
    

- <span data-ttu-id="3f4ae-150">C:\\Programme\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES</span><span class="sxs-lookup"><span data-stu-id="3f4ae-150">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES</span></span> 
    
  
- <span data-ttu-id="3f4ae-151">C:\\Programme\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\FEATURES\\PublishingLayouts\\en-us</span><span class="sxs-lookup"><span data-stu-id="3f4ae-151">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\FEATURES\\PublishingLayouts\\en-us</span></span>
    
  
<span data-ttu-id="3f4ae-p114">Da das RichHtmlField im Browser CSS verwendet, um die Formatvorlagen zu implementieren, können Sie Ihre eigenen Formatvorlagen erstellen, die konsistent mit dem Branding Ihrer Website sind, und dann diese Formatvorlagen für Inhaltsautoren auf dem Menüband verfügbar machen. Wenn Sie geringfügige Änderungen an den Standardformatvorlagen vornehmen möchten, können Sie eine vorhandene Formatvorlage aus HtmlEditorStyles.css in das Stylesheet kopieren, auf das vom Seitenlayout verwiesen wird, und dann diese Formatvorlage bearbeiten, indem Sie die CSS-Eigenschaften und -Werte (jedoch nicht die Auswahl) ändern. Sie können Standardformatvorlagen auch auf dem Menüband ausblenden, indem Sie sie in Ihr Stylesheet kopieren und anschließend  `display:none` festlegen.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p114">Because the RichHtmlField in the browser uses CSS to implement its styles, you can create your own styles that are consistent with the branding of your site, and then you can make those styles available on the ribbon for content authors to use. To make minor changes to the default styles, you can copy an existing style from HtmlEditorStyles.css to your style sheet that is referenced by the page layout, and then modify that style by changing the CSS properties and values (but not the selector). You can also hide default styles from the ribbon by copying them to your style sheet and then setting  `display:none`.</span></span>
  
    
    
<span data-ttu-id="3f4ae-p115">Zum Implementieren benutzerdefinierter Formatvorlagen können Sie auch ein Stylesheet von Grund auf neu erstellen, indem Sie die Eigenschaft **PrefixStyleSheet** für den RichHtmlField-Codeausschnitt ändern. Standardmäßig ist diese Eigenschaft auf **ms-rte** festgelegt, und die Formatvorlagen im Standardstylesheet HtmlEditorStyles.css beginnen jeweils mit dem folgenden Präfix - z. B.:</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p115">To implement custom styles, you can also build a style sheet from scratch by changing the **PrefixStyleSheet** property for the RichHtmlField snippet. By default, this property is set to **ms-rte**, and the styles in the default style sheet HtmlEditorStyles.css each begin with this prefix—for example:</span></span>
  
    
    



```HTML

H1. ms-rteElement-H1
{
-ms-name:"Heading 1";
-ms-element:"true";
}
```

<span data-ttu-id="3f4ae-p116">Wenn Sie den Wert der Eigenschaft **PrefixStyleSheet** ändern, sind keine der vorhandenen **ms-rte**-Formatvorlagen im Rich-HTML-Editor verfügbar, und nur erstellte Formatvorlagen, die das neue Präfix verwenden, stehen für Inhaltsautoren zur Verfügung. Das bedeutet, dass Sie, wenn Sie einige der Standardformatvorlagen verwenden möchten, diese in Ihr Stylesheet kopieren und ändern müssen, dass sie das neue Präfix verwenden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p116">When you change the value of the **PrefixStyleSheet** property, none of the existing **ms-rte** styles are available in the rich HTML editor, and only styles that you create that use the new prefix are available to content authors. This means if you want to use some of the default styles, they must be copied to your style sheet and modified so that they use the new prefix.</span></span>
  
> [!NOTE]
> <span data-ttu-id="3f4ae-159">Die **PrefixStyleSheet**-Eigenschaft wird pro RichHtmlField-Seitenfeld definiert, mehrere Seitenfelder können aber denselben Wert für diese Eigenschaft verwenden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-159">Note: The **PrefixStyleSheet** property is defined per each RichHtmlField page field, but multiple page fields can use the same value for this property.</span></span> <span data-ttu-id="3f4ae-160">Wenn also mehrere Seitenlayouts auf dieselbe Formatvorlage verweisen, kann es vorkommen, dass mehrere RichHtmlFields auf diesen Seitenlayouts dasselbe Formatvorlagenpräfix aufweisen und auf dieselben Formatvorlagen verweisen.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-160">So, if multiple page layouts reference the same style sheet, it's possible for multiple RichHtmlFields on those page layouts to have the same style prefix and reference the same styles.</span></span>
  
    
    


### <a name="to-define-a-new-list-of-styles-for-a-richhtmlfield"></a><span data-ttu-id="3f4ae-161">So definieren Sie eine neue Liste von Formatvorlagen für ein RichHtmlField</span><span class="sxs-lookup"><span data-stu-id="3f4ae-161">To define a new list of styles for a RichHtmlField</span></span>


1. <span data-ttu-id="3f4ae-162">Wechseln Sie zu Ihrer Veröffentlichungswebsite.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-162">Browse to your publishing site.</span></span>
    
  
2. <span data-ttu-id="3f4ae-163">Wählen Sie in der rechten oberen Ecke der Seite **Einstellungen** und dann **Entwurfs-Manager**.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-163">In the upper-right corner of the page, choose **Settings**, and then choose **Design Manager**.</span></span>
    
  
3. <span data-ttu-id="3f4ae-164">Wählen Sie im Entwurfs-Manager im linken Navigationsbereich **Seitenlayouts bearbeiten** aus.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-164">In Design Manager, in the left navigation pane, choose **Edit Page Layouts**.</span></span>
    
  
4. <span data-ttu-id="3f4ae-165">Wählen Sie das Seitenlayout aus, auf dem sich das RichHtmlField-Seitenfeld befinden soll.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-165">Choose the page layout on which the RichHtmlField page field will reside.</span></span>
    
  
5. <span data-ttu-id="3f4ae-166">Wählen Sie in der oberen rechten Ecke der serverseitigen Vorschau **Codeausschnittkatalog** aus.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-166">In the upper-right corner of the server-side preview, choose **Snippet Gallery**.</span></span>
    
  
6. <span data-ttu-id="3f4ae-167">Wählen Sie auf dem Menüband **Seitenfelder** und dann ein Seitenfeld vom Typ **RichHtmlField** aus.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-167">On the ribbon, choose **Page Fields**, and then choose a page field of the type **RichHtmlField**.</span></span>
    
  
7. <span data-ttu-id="3f4ae-168">Erweitern Sie im Eigenschaftenraster den Abschnitt **Verschiedenes**, und ändern Sie die Eigenschaft **PrefixStyleSheet** auf einen anderen Wert als **ms-rte** - z. B. auf **customstyle**.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-168">In the property grid, expand the **Misc** section, and then change the **PrefixStyleSheet** property to a value other than **ms-rte**—for example, change the value to be **customstyle**.</span></span>
    
    > <span data-ttu-id="3f4ae-169">**Wichtig**: Dieser Wert muss in Kleinbuchstaben eingegeben werden.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-169">**Important:** This property value must be all lowercase.</span></span> 
8. <span data-ttu-id="3f4ae-170">Wählen Sie **Aktualisieren** aus.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-170">Choose **Update**.</span></span>
    
  
9. <span data-ttu-id="3f4ae-171">Wählen Sie auf der linken Seite des Codeausschnittkatalogs **In die Zwischenablage kopieren** aus.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-171">On the left side of the Snippet Gallery, choose **Copy to Clipboard**.</span></span>
    
  
10. <span data-ttu-id="3f4ae-172">Öffnen Sie im zugeordneten Netzwerklaufwerk auf Ihrem Computer das HTML-Seitenlayout im HTML-Editor.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-172">In the mapped network drive on your computer, open the HTML page layout in your HTML editor.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3f4ae-173">Weitere Informationen finden Sie unter  [Gewusst wie: Zuordnen eines Netzlaufwerks zum SharePoint-Gestaltungsvorlagenkatalog](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="3f4ae-173">For more information, see  [How to: Map a network drive to the SharePoint Master Page Gallery](how-to-map-a-network-drive-to-the-sharepoint-master-page-gallery.md).</span></span> 

11. <span data-ttu-id="3f4ae-174">Fügen Sie im HTML-Seitenlayout den HTML-Codeausschnitt in **PlaceHolderMain** ein.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-174">In the HTML page layout, paste the HTML snippet inside **PlaceHolderMain**.</span></span>
    
  
12. <span data-ttu-id="3f4ae-p118">Speichern Sie das HTML-Seitenlayout. Die Änderungen an der HTML-Datei werden mit dem zugehörigen ASPX-Seitenlayout synchronisiert.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p118">Save the HTML page layout. The changes to the HTML file are synced to the associated .aspx page layout.</span></span>
    
    <span data-ttu-id="3f4ae-177">Wenn ein Inhaltsautor an diesem Punkt eine Seite auf der Basis dieses Seitenlayouts erstellt oder bearbeitet, sind keine Formatvorlagen auf dem Menüband des HTML-Editors verfügbar, da dieses bestimmte Seitenfeld nur Formatvorlagen verwendet, die mit dem neuen Präfix **customstyle** beginnen, aber diese Formatvorlagen wurden noch nicht definiert.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-177">At this point, if a content author creates or edits a page based on this page layout, no styles are available on the ribbon of the HTML editor because this specific page field uses only styles that begin with the new prefix **customstyle**, but those styles have not yet been defined.</span></span>
    
  
13. <span data-ttu-id="3f4ae-178">Navigieren Sie auf dem Server zum folgenden Speicherort, und öffnen Sie HtmlEditorStyles.css:</span><span class="sxs-lookup"><span data-stu-id="3f4ae-178">On the server, browse to the following location and open HtmlEditorStyles.css:</span></span>
    
    <span data-ttu-id="3f4ae-179">C:\\Programme\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES</span><span class="sxs-lookup"><span data-stu-id="3f4ae-179">C:\\Program Files\\Common Files\\Microsoft Shared\\Web Server Extensions\\15\\TEMPLATE\\LAYOUTS\\1033\\STYLES</span></span>
    
    <span data-ttu-id="3f4ae-p119">Es ist nützlich, die Standardformatvorlagen anzuzeigen, zu verstehen, wie sie geschrieben werden, und möglicherweise einige davon wiederzuverwenden, indem Sie sie in Ihre Stylesheet kopieren und dann ändern. Wenn Sie dies tun, ersetzen Sie das Standard- **ms Rte** -Präfix durch Ihr eigenes Präfix.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-p119">It's useful to view the default styles, understand how they're written, and possibly reuse some of them by copying them to your style sheet and then modifying them. If you do this, replace the default **ms-rte** prefix with your own prefix.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="3f4ae-182">Ändern Sie nicht die Standardformatvorlage „HtmlEditorStyles.css“.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-182">Important: Do not modify the default style sheet, HtmlEditorStyles.css.</span></span> <span data-ttu-id="3f4ae-183">Dieses Stylesheet enthält Formatvorlagen für jedes RichHtmlField in der Farm.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-183">This style sheet provides styles for every RichHtmlField in the farm.</span></span> <span data-ttu-id="3f4ae-184">Außerdem kann diese Datei von Dienstupdates oder Upgrades überschrieben werden, sodass alle Änderungen verloren gehen.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-184">Also, service updates or an upgrade may overwrite this file, causing you to lose any changes.</span></span> 

14. <span data-ttu-id="3f4ae-185">Erstellen Sie in der Formatvorlage eine Liste neuer Formatvorlagen, die mit dem neuen Präfix beginnen.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-185">In your style sheet, create a list of new styles that start with the new prefix.</span></span>
    
    <span data-ttu-id="3f4ae-186">Wenn beispielsweise **customstyle** das neue Präfix ist, enthält Ihr Stylesheet möglicherweise die folgende Formatvorlage.</span><span class="sxs-lookup"><span data-stu-id="3f4ae-186">For example, if **customstyle** is the new prefix, your style sheet might contain the following style.</span></span>
    


```HTML
  
H2.customstyleElement-H2
{
-ms-name:"Heading 2";
-ms-element:"true";
}
customstyleElement-H2
{
font-weight: bold;
font-family: Cambria;
font-size: 16pt;
} 

```


    For clarity, the class name and the name of the style as it appears on the ribbon are defined separately from the style properties. In this example, **H2** is the element selector for the style, and **customstyleElement-H2** is the class name of the style. The class name has two parts: **customstyle** is the prefix that you specified for this page field, and **Element** specifies that this style will appear in the **Page Elements** section of the **Styles** gallery on the ribbon of the HTML editor. The **-ms-name** property sets the display name that appears to content authors in the Styles gallery.
    
    SharePoint maps a style to a menu or command on the ribbon by parsing the class name immediately after the prefix and looking for one of these strings:
    
  - <span data-ttu-id="3f4ae-187">**Element**: Der Abschnitt „Seitenelemente" des Formatvorlagenkatalogs</span><span class="sxs-lookup"><span data-stu-id="3f4ae-187">**Element**: The Page Elements section of the Styles gallery</span></span>
    
  
  - <span data-ttu-id="3f4ae-188">**Style**: Der Abschnitt „Textformatvorlagen" des Formatvorlagenkatalogs</span><span class="sxs-lookup"><span data-stu-id="3f4ae-188">**Style**: The Text Styles section of the Styles gallery</span></span>
    
  
  - <span data-ttu-id="3f4ae-189">**FontSize**: Das Menü „Schriftgrad"</span><span class="sxs-lookup"><span data-stu-id="3f4ae-189">**FontSize**: The Font Size menu</span></span>
    
  
  - <span data-ttu-id="3f4ae-190">**ThemeFontFace**: Das Menü „Schriftart"</span><span class="sxs-lookup"><span data-stu-id="3f4ae-190">**ThemeFontFace**: The Font menu</span></span>
    
  
  - <span data-ttu-id="3f4ae-191">**ForeColor**: Das Menü „Schriftfarbe"</span><span class="sxs-lookup"><span data-stu-id="3f4ae-191">**ForeColor**: The Font Color menu</span></span>
    
  
  - <span data-ttu-id="3f4ae-192">**BackColor**: Das Menü „Hervorhebungsfarbe"</span><span class="sxs-lookup"><span data-stu-id="3f4ae-192">**BackColor**: The Highlight Color menu</span></span>
    
  
  - <span data-ttu-id="3f4ae-193">**Image**: Das Menü „Grafik"</span><span class="sxs-lookup"><span data-stu-id="3f4ae-193">**Image**: The Image menu</span></span>
    
  
  - <span data-ttu-id="3f4ae-194">**Table**: Das Menü „Tabelle"</span><span class="sxs-lookup"><span data-stu-id="3f4ae-194">**Table**: The Table menu</span></span>
    
  
  - <span data-ttu-id="3f4ae-195">**Position**: Die Ausrichten-Schaltflächen in der Gruppe „Absatz"'</span><span class="sxs-lookup"><span data-stu-id="3f4ae-195">**Position**: The Align buttons in the Paragraph group</span></span>
    
  

    <span data-ttu-id="3f4ae-196">Weitere Informationen dazu, wo sich Formatvorlagen für ein Seitenlayout befinden sollten, finden Sie unter  [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="3f4ae-196">For more information about where styles for a page layout should reside, see  [How to: Create a page layout in SharePoint](how-to-create-a-page-layout-in-sharepoint.md).</span></span>
    
  

## <a name="see-also"></a><span data-ttu-id="3f4ae-197">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="3f4ae-197">See also</span></span>
<span data-ttu-id="3f4ae-198"><a name="Additional"> </a></span><span class="sxs-lookup"><span data-stu-id="3f4ae-198"><a name="Additional"> </a></span></span>


-  [<span data-ttu-id="3f4ae-199">Übersicht über den Entwurfs-Manager in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3f4ae-199">Overview of Design Manager in SharePoint</span></span>](overview-of-design-manager-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3f4ae-200">Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint</span><span class="sxs-lookup"><span data-stu-id="3f4ae-200">How to: Create a page layout in SharePoint</span></span>](how-to-create-a-page-layout-in-sharepoint.md)
    
  
-  [<span data-ttu-id="3f4ae-201">Codeausschnitte des SharePoint-Entwurfs-Managers</span><span class="sxs-lookup"><span data-stu-id="3f4ae-201">SharePoint Design Manager snippets</span></span>](sharepoint-design-manager-snippets.md)
    
  

