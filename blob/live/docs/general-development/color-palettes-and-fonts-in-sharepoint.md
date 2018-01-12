---
title: Farbpaletten und Schriftarten in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: c17d375b-151f-48ae-ac32-f2ce9e68d63f
ms.openlocfilehash: 0ae750c42451986a7f3bdc50111759a69e8a84db
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="color-palettes-and-fonts-in-sharepoint"></a><span data-ttu-id="36030-102">Farbpaletten und Schriftarten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="36030-102">Color palettes and fonts in SharePoint</span></span>
<span data-ttu-id="36030-103">Verwenden Sie diese Übersicht, um die in einer SharePoint-Website verwendeten Farbpaletten oder Schriftartenschemas zu definieren.</span><span class="sxs-lookup"><span data-stu-id="36030-103">Use this reference to define the color palette or font scheme that is used in a SharePoint site.</span></span>
## <a name="color-palettes"></a><span data-ttu-id="36030-104">Farbpaletten</span><span class="sxs-lookup"><span data-stu-id="36030-104">Color palettes</span></span>
<span data-ttu-id="36030-105"><a name="color"> </a></span><span class="sxs-lookup"><span data-stu-id="36030-105"><a name="color"> </a></span></span>

<span data-ttu-id="36030-p101">Eine Farbpalette stellt die Kombination der Farben dar, die in einer SharePoint-Website verwendet werden. Die Farbpalette für eine SharePoint-Website wird in einer Farbpalettendatei definiert. Farbplätze werden auch von der Vorschaudatei für Gestaltungsvorlagen verwendet, um Miniatur- und Vorschaubilder einer Website zu erstellen. Im Folgenden wird der Aufbau der Farbpalettendatei und der Vorschaudatei für Gestaltungsvorlagen beschrieben:</span><span class="sxs-lookup"><span data-stu-id="36030-p101">A color palette is the combination of colors that are used in a SharePoint site. The color palette for a SharePoint site is defined in a color palette file. Color slots are also used by the master page preview file to generate thumbnail and preview images of a site. The following describes the structure of the color palette file and the master page preview file:</span></span>
  
    
    

- <span data-ttu-id="36030-110">**Farbpalettendatei (.spcolor)**</span><span class="sxs-lookup"><span data-stu-id="36030-110">**Color palette file (.spcolor)**</span></span>
    
    <span data-ttu-id="36030-p102">Farbpalettendateien werden im Assistenten **Aussehen ändern** verwendet, mit dem Benutzer das Erscheinungsbild ihrer Website mithilfe der SharePoint-Designbenutzeroberfläche ändern können. Mit SharePoint werden standardmäßig 32 Farbpalettendateien installiert. Sie können auch zusätzliche Farbpalettendateien erstellen. Das folgende Beispiel zeigt das Format einer Farbpalettendatei.</span><span class="sxs-lookup"><span data-stu-id="36030-p102">Color palette files are used in the **Change the look** wizard, which enables users to change the look and feel of their site by using the SharePoint themes user interface. By default, 32 color palette files are installed with SharePoint. You can also create additional color palette files. The following example shows the format of a color palette file.</span></span>
    

```xml  
<s:colorPalette isInverted="InvertedSetting" previewSlot1="Slot1" previewSlot2="Slot2" previewSlot3="Slot3" xmlns:s="http://schemas.microsoft.com/sharepoint/">
    <s:color name="ColorSlot" value="Color" />
    <!--additional color slots-->
</s:colorPalette>
```


  <span data-ttu-id="36030-115">In einer Farbpalettendatei werden die folgenden Platzhalter ersetzt:</span><span class="sxs-lookup"><span data-stu-id="36030-115">In a color palette file, the following placeholders are replaced:</span></span>
    
-  <span data-ttu-id="36030-p103">_InvertedSetting_ ist ein Boolescher Wert. **true**, wenn die Farbpalette in der Regel hellen Text vor dunklem Hintergrund umfasst. **false**, wenn die Farbpalette in der Regel dunklen Text vor hellem Hintergrund umfasst.</span><span class="sxs-lookup"><span data-stu-id="36030-p103">_InvertedSetting_ is a Boolean value. **true** if the color palette is generally light text on a dark background. **false** if the color palette is generally dark text on a light background.</span></span>
    
  
-  <span data-ttu-id="36030-119">_Slot1_ ist der Anmerkungsname des Farbplatzes, der in der Farbpalettenauswahl der Designoberfläche als der erste Block des Palettensymbols verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="36030-119">_Slot1_ is the annotation name of the color slot to use as the first block of the palette icon in the color palette picker of the theming experience.</span></span>
    
  
-  <span data-ttu-id="36030-120">_Slot2_ ist der Anmerkungsname des Farbplatzes, der in der Farbpalettenauswahl der Designoberfläche als der zweite Block des Palettensymbols verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="36030-120">_Slot2_ is the annotation name of the color slot to use as the second block of the palette icon in the color palette picker of the theming experience.</span></span>
    
  
-  <span data-ttu-id="36030-121">_Slot3_ ist der Anmerkungsname des Farbplatzes, der in der Farbpalettenauswahl der Designoberfläche als der dritte Block des Palettensymbols verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="36030-121">_Slot3_ is the annotation name of the color slot to use as the third block of the palette icon in the color palette picker of the theming experience.</span></span>
    
  
-  <span data-ttu-id="36030-122">_ColorSlot_ ist der Anmerkungsname des Farbplatzes, den Sie definieren (z. B. Websitetitel).</span><span class="sxs-lookup"><span data-stu-id="36030-122">_ColorSlot_ is the annotation name of the color slot that you are defining (for example, SiteTitle).</span></span>
    
  
-  <span data-ttu-id="36030-p104">_Color_ ist der Hexadezimalwert der Farbe, die für den angegebenen Farbplatz verwendet werden soll. Er kann sechsstellig (RRGGBB) oder achtstellig (AARRGGBB) sein. Wenn der Hexadezimalwert achtstellig ist, geben die ersten beiden Stellen die Transparenzstufe (00-FF, was 0-255 entspricht) an. Ist der Hexadezimalwert sechsstellig, ist der Standardtransparenzwert 100 % oder FF.</span><span class="sxs-lookup"><span data-stu-id="36030-p104">_Color_ is the hexadecimal value of the color to use for the specified color slot. This may be in 6 digits (RRGGBB) or 8 digits (AARRGGBB). If the hexadecimal value is 8 digits, the first two digits represent the opacity level (00-FF, which maps to 0-255). If the hexadecimal value is 6 digits, the default opacity is 100% or FF.</span></span>
    
  

  <span data-ttu-id="36030-p105">Die Farbpalettendateien sich im Designkatalog der Stammwebsite gespeichert, in der Websitesammlung im Ordner **15** (http:// _SiteCollectionName_/_catalogs/theme/15/). Um den Designkatalog über die Benutzerfläche von SharePoint aufzurufen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** **Designs** und dann **15** aus.</span><span class="sxs-lookup"><span data-stu-id="36030-p105">The color palette files are located in the Theme Gallery of the root site, in the site collection in the **15** folder (http:// _SiteCollectionName_/_catalogs/theme/15/). To access the Theme Gallery from the SharePoint user interface, on the **Site Settings** page, under **Web Designer Galleries**, select **Themes**, and then select **15**.</span></span>
    
  
- <span data-ttu-id="36030-129">**Vorschaudatei für Gestaltungsvorlagen (.preview)**</span><span class="sxs-lookup"><span data-stu-id="36030-129">**Master page preview file (.preview)**</span></span>
    
  <span data-ttu-id="36030-p106">Vorschaudateien für Gestaltungsvorlagen werden verwendet, um bei Verwendung des Assistenten **Aussehen ändern** Miniatur- und Vorschaubilder zu generieren. Eine Gestaltungsvorlage muss eine entsprechende Vorschaudatei aufweisen, die im Assistenten **Aussehen ändern** verwendet wird. Eine Vorschaudatei stellt eine speziell formatierte Datei dar, die Abschnitte für die Standardfarbpalette, das Standardschriftartenschema, Token-CSS und Token-HTML enthält. Sie verwendet Zeichenfolgetoken, um den Wert von Farbplätzen, Schriftartnamen und lokalisierten UI-Zeichenfolgen abzurufen. Das folgende Beispiel zeigt Farbplätze, die in der Vorschaudatei für Gestaltungsvorlagen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="36030-p106">Master page preview files are used to generate thumbnail images and preview images when you use the **Change the look** wizard. A master page must have a corresponding preview file to be used in the **Change the look** wizard. A preview file is a specially formatted file that has sections for the default color palette, default font scheme, tokenized CSS, and tokenized HTML. It uses string tokens to get the value of color slots, font names, and localized UI strings. The following example shows color slots being used in the master page preview file.</span></span>
    


```HTML
  
[ID] #dgp-pageContainer
{
    background-color: [T_THEME_COLOR_PAGEBACKGROUND];
    color: [T_THEME_COLOR_BODYTEXT];
    width: 100%;
    height:100%;     
    background-image: url('[T_IMAGE]');       
    background-size: cover;
    font-family: [T_BODY_FONT];   
}
```


  <span data-ttu-id="36030-135">Weitere Informationen finden Sie unter [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)</span><span class="sxs-lookup"><span data-stu-id="36030-135">For more information, see  [How to: Create a master page preview file in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)</span></span>
    
  

> <span data-ttu-id="36030-136">**Tipp:** Sie können das SharePoint-Farbpalettentool zum Erstellen von SharePoint-Designs verwenden.</span><span class="sxs-lookup"><span data-stu-id="36030-136">**Tip:** You can use the SharePoint color palette tool to help you create SharePoint designs.</span></span> <span data-ttu-id="36030-137">Sie können [das SharePoint-Farbpalettentool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) im Microsoft Download Center herunterladen.</span><span class="sxs-lookup"><span data-stu-id="36030-137">You can  [download the SharePoint color palette tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) from the Microsoft Download Center.</span></span>
  
    
    


### <a name="color-slot-mapping"></a><span data-ttu-id="36030-138">Farbmodul-Zuordnung</span><span class="sxs-lookup"><span data-stu-id="36030-138">Color slot mapping</span></span>
<span data-ttu-id="36030-139"><a name="colorSlots"> </a></span><span class="sxs-lookup"><span data-stu-id="36030-139"><a name="colorSlots"> </a></span></span>

<span data-ttu-id="36030-140">Tabelle 1 beschreibt die verfügbaren Farbmodule und wo diese Farbmodule auf einer SharePoint-Website verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="36030-140">Table 1 describes the color slots that are available and where color slots are used in a SharePoint site.</span></span>
  
> [!NOTE]
> <span data-ttu-id="36030-141">Bei der Erläuterung von Navigationselementen bedeutet „Pressed“ (Gedrückt), dass ein Benutzer auf ein Navigationselement klickt oder es berührt. „Selected“ (Ausgewählt) bezieht sich darauf, dass ein Benutzer auf die Seite geleitet wird.> Nachfolgend finden Sie eine Zusammenfassung einer normalen Aktionenfolge und des Farbmoduls für den Navigationselement-Link in jedem Schritt:> Der Basistext eines Navigationselement-Links: HeaderNavigationText> Ein Benutzer bewegt den Cursor über den Navigationselement-Link: HeaderNavigationHoverText> Ein Benutzer klickt auf, berührt oder wählt den Navigationselement-Link: HeaderNavigationPressedText> Der Benutzer wird auf die ausgewählten Seite geleitet.</span><span class="sxs-lookup"><span data-stu-id="36030-141">Note: When discussing navigation items,pressed applies to when a user clicks or touches a navigation item.Selected applies to when a user is navigated to the page.>  The following summarizes a normal flow of actions and the color slot that applies to the navigation item link at each step:>  The base text of a navigation item link: HeaderNavigationText>  A user hovers the cursor over the navigation item link: HeaderNavigationHoverText>  A user clicks, touches, or chooses the navigation item link: HeaderNavigationPressedText>  The user is navigated to the chosen page.</span></span> <span data-ttu-id="36030-142">Das Farbmodul, das sich auf das Navigationselement für die Seite bezieht, auf der sich der Benutzer nun befindet: HeaderNavigationSelectedText</span><span class="sxs-lookup"><span data-stu-id="36030-142">The color slot that applies to the navigation item for the page the user is now on: HeaderNavigationSelectedText</span></span>
  
    
    


<span data-ttu-id="36030-143">**Tabelle 1. Farbmodule**</span><span class="sxs-lookup"><span data-stu-id="36030-143">**Table 1. Color slots**</span></span>


|<span data-ttu-id="36030-144">**Anmerkungsname**</span><span class="sxs-lookup"><span data-stu-id="36030-144">**Annotation Name**</span></span>|<span data-ttu-id="36030-145">**Wo die Farbe in der UI verwendet wird**</span><span class="sxs-lookup"><span data-stu-id="36030-145">**Where the Color Is Used in the UI**</span></span>|<span data-ttu-id="36030-146">**Tokenname**</span><span class="sxs-lookup"><span data-stu-id="36030-146">**Token Name**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="36030-147">BodyText</span><span class="sxs-lookup"><span data-stu-id="36030-147">BodyText</span></span>  <br/> |<span data-ttu-id="36030-148">Normaler Textkörper</span><span class="sxs-lookup"><span data-stu-id="36030-148">Normal body text.</span></span>  <br/> |<span data-ttu-id="36030-149">[T_THEME_COLOR_BODYTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-149">[T_THEME_COLOR_BODYTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-150">SubtleBodyText</span><span class="sxs-lookup"><span data-stu-id="36030-150">SubtleBodyText</span></span>  <br/> |<span data-ttu-id="36030-p109">Textkörper, der heller als normal sein muss, wie z. B. Metadatentext</span><span class="sxs-lookup"><span data-stu-id="36030-p109">Body text that must be lighter than normal. An example is metadata text.</span></span>  <br/> |<span data-ttu-id="36030-153">[T_THEME_COLOR_SUBTLEBODYTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-153">[T_THEME_COLOR_SUBTLEBODYTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-154">StrongBodyText</span><span class="sxs-lookup"><span data-stu-id="36030-154">StrongBodyText</span></span>  <br/> |<span data-ttu-id="36030-155">Textkörperfarbe für Text, der sich vom normalen Textkörper abheben muss</span><span class="sxs-lookup"><span data-stu-id="36030-155">Body text color for text that must stand out from normal body text.</span></span>  <br/> |<span data-ttu-id="36030-156">[T_THEME_COLOR_STRONGBODYTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-156">[T_THEME_COLOR_STRONGBODYTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-157">DisabledText</span><span class="sxs-lookup"><span data-stu-id="36030-157">DisabledText</span></span>  <br/> |<span data-ttu-id="36030-p110">Deaktivierter Text, z. B. nicht verfügbare Elemente in Menüs</span><span class="sxs-lookup"><span data-stu-id="36030-p110">Disabled text. For example, unavailable items in menus.</span></span>  <br/> |<span data-ttu-id="36030-160">[T_THEME_COLOR_DISABLEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-160">[T_THEME_COLOR_DISABLEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-161">SiteTitle</span><span class="sxs-lookup"><span data-stu-id="36030-161">SiteTitle</span></span>  <br/> |<span data-ttu-id="36030-162">Die Textfarbe des Seitentitels</span><span class="sxs-lookup"><span data-stu-id="36030-162">The text color of the page title.</span></span>  <br/> |<span data-ttu-id="36030-163">[T_THEME_COLOR_SITETITLE]</span><span class="sxs-lookup"><span data-stu-id="36030-163">[T_THEME_COLOR_SITETITLE]</span></span>  <br/> |
|<span data-ttu-id="36030-164">WebPartHeading</span><span class="sxs-lookup"><span data-stu-id="36030-164">WebPartHeading</span></span>  <br/> |<span data-ttu-id="36030-165">Textfarbe für Webpart-Überschriften</span><span class="sxs-lookup"><span data-stu-id="36030-165">Text color for Web Part headings.</span></span>  <br/> |<span data-ttu-id="36030-166">[T_THEME_COLOR_WEBPARTHEADING]</span><span class="sxs-lookup"><span data-stu-id="36030-166">[T_THEME_COLOR_WEBPARTHEADING]</span></span>  <br/> |
|<span data-ttu-id="36030-167">ErrorText</span><span class="sxs-lookup"><span data-stu-id="36030-167">ErrorText</span></span>  <br/> |<span data-ttu-id="36030-168">Die Hauptfarbe für Text, Rahmen und Hintergründe, die sich auf Fehler beziehen (nach Bedarf)</span><span class="sxs-lookup"><span data-stu-id="36030-168">The main error color that is used for error text, borders, and backgrounds, as needed.</span></span>  <br/> |<span data-ttu-id="36030-169">[T_THEME_COLOR_ERRORTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-169">[T_THEME_COLOR_ERRORTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-170">AccentText</span><span class="sxs-lookup"><span data-stu-id="36030-170">AccentText</span></span>  <br/> |<span data-ttu-id="36030-171">Textfarbe für hervorgehobenen Textkörper</span><span class="sxs-lookup"><span data-stu-id="36030-171">Text color for accented body text.</span></span>  <br/> |<span data-ttu-id="36030-172">[T_THEME_COLOR_ACCENTTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-172">[T_THEME_COLOR_ACCENTTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-173">SearchURL</span><span class="sxs-lookup"><span data-stu-id="36030-173">SearchURL</span></span>  <br/> |<span data-ttu-id="36030-p111">Textfarbe für die in Suchergebnissen gefundene URL. Wird auch zum Hervorheben neuer Elemente oder Erfolgsstatusmeldungen verwendet.</span><span class="sxs-lookup"><span data-stu-id="36030-p111">Text color for the URL found in search results. Also used to highlight new items or successful status notifications.</span></span>  <br/> |<span data-ttu-id="36030-176">[T_THEME_COLOR_SEARCHURL]</span><span class="sxs-lookup"><span data-stu-id="36030-176">[T_THEME_COLOR_SEARCHURL]</span></span>  <br/> |
|<span data-ttu-id="36030-177">Hyperlink</span><span class="sxs-lookup"><span data-stu-id="36030-177">Hyperlink</span></span>  <br/> |<span data-ttu-id="36030-178">Textfarbe für Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="36030-178">Text color for hyperlinks.</span></span>  <br/> |<span data-ttu-id="36030-179">[T_THEME_COLOR_HYPERLINK]</span><span class="sxs-lookup"><span data-stu-id="36030-179">[T_THEME_COLOR_HYPERLINK]</span></span>  <br/> |
|<span data-ttu-id="36030-180">HyperlinkFollowed</span><span class="sxs-lookup"><span data-stu-id="36030-180">HyperlinkFollowed</span></span>  <br/> |<span data-ttu-id="36030-181">Textfarbe für gefolgte Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="36030-181">Text color for followed hyperlinks.</span></span>  <br/> |<span data-ttu-id="36030-182">[T_THEME_COLOR_HYPERLINKFOLLOWED]</span><span class="sxs-lookup"><span data-stu-id="36030-182">[T_THEME_COLOR_HYPERLINKFOLLOWED]</span></span>  <br/> |
|<span data-ttu-id="36030-183">HyperlinkActive</span><span class="sxs-lookup"><span data-stu-id="36030-183">HyperlinkActive</span></span>  <br/> |<span data-ttu-id="36030-184">Hyperlinkfarbe, wenn Hyperlink gedrückt wird</span><span class="sxs-lookup"><span data-stu-id="36030-184">Hyperlink color when pressed.</span></span>  <br/> |<span data-ttu-id="36030-185">[T_THEME_COLOR_HYPERLINKACTIVE]</span><span class="sxs-lookup"><span data-stu-id="36030-185">[T_THEME_COLOR_HYPERLINKACTIVE]</span></span>  <br/> |
|<span data-ttu-id="36030-186">CommandLinks</span><span class="sxs-lookup"><span data-stu-id="36030-186">CommandLinks</span></span>  <br/> |<span data-ttu-id="36030-187">Große Befehlslinks, die aufgrund ihrer Größe ein bisschen heller sein müssen als der Textkörper</span><span class="sxs-lookup"><span data-stu-id="36030-187">Large command links that must be a bit lighter than body text because of their size.</span></span>  <br/> |<span data-ttu-id="36030-188">[T_THEME_COLOR_COMMANDLINKS]</span><span class="sxs-lookup"><span data-stu-id="36030-188">[T_THEME_COLOR_COMMANDLINKS]</span></span>  <br/> |
|<span data-ttu-id="36030-189">CommandLinksSecondary</span><span class="sxs-lookup"><span data-stu-id="36030-189">CommandLinksSecondary</span></span>  <br/> |<span data-ttu-id="36030-190">Befehlslinkfarbe für Links, die kleiner sind und daher eine stärkere Farbe aufweisen, um hervorzutreten</span><span class="sxs-lookup"><span data-stu-id="36030-190">Command link color for links that are smaller, and therefore have a stronger color to stand out.</span></span>  <br/> |<span data-ttu-id="36030-191">[T_THEME_COLOR_COMMANDLINKSSECONDARY]</span><span class="sxs-lookup"><span data-stu-id="36030-191">[T_THEME_COLOR_COMMANDLINKSSECONDARY]</span></span>  <br/> |
|<span data-ttu-id="36030-192">CommandLinksHover</span><span class="sxs-lookup"><span data-stu-id="36030-192">CommandLinksHover</span></span>  <br/> |<span data-ttu-id="36030-193">Befehlslinkfarbe beim Daraufzeigen</span><span class="sxs-lookup"><span data-stu-id="36030-193">Command link color on hover.</span></span>  <br/> |<span data-ttu-id="36030-194">[T_THEME_COLOR_COMMANDLINKSHOVER]</span><span class="sxs-lookup"><span data-stu-id="36030-194">[T_THEME_COLOR_COMMANDLINKSHOVER]</span></span>  <br/> |
|<span data-ttu-id="36030-195">CommandLinksPressed</span><span class="sxs-lookup"><span data-stu-id="36030-195">CommandLinksPressed</span></span>  <br/> |<span data-ttu-id="36030-196">Befehlslinkfarbe, wenn Befehlslink gedrückt wird</span><span class="sxs-lookup"><span data-stu-id="36030-196">Command link color when pressed.</span></span>  <br/> |<span data-ttu-id="36030-197">[T_THEME_COLOR_COMMANDLINKSPRESSED]</span><span class="sxs-lookup"><span data-stu-id="36030-197">[T_THEME_COLOR_COMMANDLINKSPRESSED]</span></span>  <br/> |
|<span data-ttu-id="36030-198">CommandLinksDisabled</span><span class="sxs-lookup"><span data-stu-id="36030-198">CommandLinksDisabled</span></span>  <br/> |<span data-ttu-id="36030-199">Befehlslinkfarbe, wenn Befehlslink deaktiviert ist</span><span class="sxs-lookup"><span data-stu-id="36030-199">Command link color when command link is disabled.</span></span>  <br/> |<span data-ttu-id="36030-200">[T_THEME_COLOR_COMMANDLINKSDISABLED]</span><span class="sxs-lookup"><span data-stu-id="36030-200">[T_THEME_COLOR_COMMANDLINKSDISABLED]</span></span>  <br/> |
|<span data-ttu-id="36030-201">BackgroundOverlay</span><span class="sxs-lookup"><span data-stu-id="36030-201">BackgroundOverlay</span></span>  <br/> |<span data-ttu-id="36030-202">Die Haupthintergrundfarbe, die zwischen dem optionalen Hintergrundbild und dem Seiteninhalt sichtbar ist</span><span class="sxs-lookup"><span data-stu-id="36030-202">The main background color that is visible between the optional background image and the page content.</span></span>  <br/> |<span data-ttu-id="36030-203">[T_THEME_COLOR_BACKGROUNDOVERLAY]</span><span class="sxs-lookup"><span data-stu-id="36030-203">[T_THEME_COLOR_BACKGROUNDOVERLAY]</span></span>  <br/> |
|<span data-ttu-id="36030-204">DisabledBackground</span><span class="sxs-lookup"><span data-stu-id="36030-204">DisabledBackground</span></span>  <br/> |<span data-ttu-id="36030-205">Hintergrund für deaktivierte Elemente wie Browsersteuerelemente, z. B. Eingabe- oder Auswahlfeld (außer Schaltflächen)</span><span class="sxs-lookup"><span data-stu-id="36030-205">Background for disabled elements such as browser controls, for example, input box or select box (except buttons).</span></span>  <br/> |<span data-ttu-id="36030-206">[T_THEME_COLOR_DISABLEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-206">[T_THEME_COLOR_DISABLEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-207">PageBackground</span><span class="sxs-lookup"><span data-stu-id="36030-207">PageBackground</span></span>  <br/> |<span data-ttu-id="36030-p112">Die Hintergrundfarbe der Seite. Erscheint hinter dem optionalen Hintergrundbild.</span><span class="sxs-lookup"><span data-stu-id="36030-p112">The background color of the page. Appears behind the optional background image.</span></span>  <br/> |<span data-ttu-id="36030-210">[T_THEME_COLOR_PAGEBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-210">[T_THEME_COLOR_PAGEBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-211">HeaderBackground</span><span class="sxs-lookup"><span data-stu-id="36030-211">HeaderBackground</span></span>  <br/> |<span data-ttu-id="36030-212">Die Hintergrundfarbe für den Kopfbereich der Seite</span><span class="sxs-lookup"><span data-stu-id="36030-212">The background color for the header area of the page.</span></span>  <br/> |<span data-ttu-id="36030-213">[T_THEME_COLOR_HEADERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-213">[T_THEME_COLOR_HEADERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-214">FooterBackground</span><span class="sxs-lookup"><span data-stu-id="36030-214">FooterBackground</span></span>  <br/> |<span data-ttu-id="36030-215">Die Hintergrundfarbe für den Fußzeilenbereich der Seite</span><span class="sxs-lookup"><span data-stu-id="36030-215">The background color for the footer area of the page.</span></span>  <br/> |<span data-ttu-id="36030-216">[T_THEME_COLOR_FOOTERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-216">[T_THEME_COLOR_FOOTERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-217">SelectionBackground</span><span class="sxs-lookup"><span data-stu-id="36030-217">SelectionBackground</span></span>  <br/> |<span data-ttu-id="36030-218">Die Hintergrundfarbe für ausgewählte Listenelemente und Dropdownmenü-Elemente</span><span class="sxs-lookup"><span data-stu-id="36030-218">The background color for selected list items and drop-down menu items.</span></span>  <br/> |<span data-ttu-id="36030-219">[T_THEME_COLOR_SELECTIONBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-219">[T_THEME_COLOR_SELECTIONBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-220">HoverBackground</span><span class="sxs-lookup"><span data-stu-id="36030-220">HoverBackground</span></span>  <br/> |<span data-ttu-id="36030-221">Die Hintergrundfarbe für Listenelemente und Dropdownmenü-Elemente beim Daraufzeigen</span><span class="sxs-lookup"><span data-stu-id="36030-221">The background color for list items and drop-down menu items on hover.</span></span>  <br/> |<span data-ttu-id="36030-222">[T_THEME_COLOR_HOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-222">[T_THEME_COLOR_HOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-223">RowAccent</span><span class="sxs-lookup"><span data-stu-id="36030-223">RowAccent</span></span>  <br/> |<span data-ttu-id="36030-224">Der hervorgehobene linke Rand bei ausgewählten Listenelementen</span><span class="sxs-lookup"><span data-stu-id="36030-224">The accented left border on selected list items.</span></span>  <br/> |<span data-ttu-id="36030-225">[T_THEME_COLOR_ROWACCENT]</span><span class="sxs-lookup"><span data-stu-id="36030-225">[T_THEME_COLOR_ROWACCENT]</span></span>  <br/> |
|<span data-ttu-id="36030-226">StrongLines</span><span class="sxs-lookup"><span data-stu-id="36030-226">StrongLines</span></span>  <br/> |<span data-ttu-id="36030-227">Rahmen für Browsersteuerelemente beim Daraufzeigen</span><span class="sxs-lookup"><span data-stu-id="36030-227">Borders for browser controls on hover.</span></span>  <br/> |<span data-ttu-id="36030-228">[T_THEME_COLOR_STRONGLINES]</span><span class="sxs-lookup"><span data-stu-id="36030-228">[T_THEME_COLOR_STRONGLINES]</span></span>  <br/> |
|<span data-ttu-id="36030-229">Lines</span><span class="sxs-lookup"><span data-stu-id="36030-229">Lines</span></span>  <br/> |<span data-ttu-id="36030-230">Rahmen für Browsersteuerelemente</span><span class="sxs-lookup"><span data-stu-id="36030-230">Borders for browser controls.</span></span>  <br/> |<span data-ttu-id="36030-231">[T_THEME_COLOR_LINES]</span><span class="sxs-lookup"><span data-stu-id="36030-231">[T_THEME_COLOR_LINES]</span></span>  <br/> |
|<span data-ttu-id="36030-232">SubtleLines</span><span class="sxs-lookup"><span data-stu-id="36030-232">SubtleLines</span></span>  <br/> |<span data-ttu-id="36030-p113">Farbe für dezente Rahmen, z. B. Rasterlinien für Inlinebearbeitung</span><span class="sxs-lookup"><span data-stu-id="36030-p113">Subtle border color. For example, gridlines for inline editing.</span></span>  <br/> |<span data-ttu-id="36030-235">[T_THEME_COLOR_SUBTLELINES]</span><span class="sxs-lookup"><span data-stu-id="36030-235">[T_THEME_COLOR_SUBTLELINES]</span></span>  <br/> |
|<span data-ttu-id="36030-236">DisabledLines</span><span class="sxs-lookup"><span data-stu-id="36030-236">DisabledLines</span></span>  <br/> |<span data-ttu-id="36030-237">Rahmenfarbe für deaktivierte Browsersteuerelemente wie Eingabe- und Auswahlfelder</span><span class="sxs-lookup"><span data-stu-id="36030-237">Border color for disabled browser controls such as input boxes and select boxes.</span></span>  <br/> |<span data-ttu-id="36030-238">[T_THEME_COLOR_DISABLEDLINES]</span><span class="sxs-lookup"><span data-stu-id="36030-238">[T_THEME_COLOR_DISABLEDLINES]</span></span>  <br/> |
|<span data-ttu-id="36030-239">AccentLines</span><span class="sxs-lookup"><span data-stu-id="36030-239">AccentLines</span></span>  <br/> |<span data-ttu-id="36030-240">Farbe für fokussierte Rahmen bei ausgewählten Browsersteuerelementen</span><span class="sxs-lookup"><span data-stu-id="36030-240">Focused border color for selected browser controls.</span></span>  <br/> |<span data-ttu-id="36030-241">[T_THEME_COLOR_ACCENTLINES]</span><span class="sxs-lookup"><span data-stu-id="36030-241">[T_THEME_COLOR_ACCENTLINES]</span></span>  <br/> |
|<span data-ttu-id="36030-242">DialogBorder</span><span class="sxs-lookup"><span data-stu-id="36030-242">DialogBorder</span></span>  <br/> |<span data-ttu-id="36030-243">Farbe für Dialogfeldrahmen</span><span class="sxs-lookup"><span data-stu-id="36030-243">Dialog box border color.</span></span>  <br/> |<span data-ttu-id="36030-244">[T_THEME_COLOR_DIALOGBORDER]</span><span class="sxs-lookup"><span data-stu-id="36030-244">[T_THEME_COLOR_DIALOGBORDER]</span></span>  <br/> |
|<span data-ttu-id="36030-245">Navigation</span><span class="sxs-lookup"><span data-stu-id="36030-245">Navigation</span></span>  <br/> |<span data-ttu-id="36030-246">Textfarbe für horizontale und vertikale Navigationselemente</span><span class="sxs-lookup"><span data-stu-id="36030-246">Text color for horizontal and vertical navigation items.</span></span>  <br/> |<span data-ttu-id="36030-247">[T_THEME_COLOR_NAVIGATION]</span><span class="sxs-lookup"><span data-stu-id="36030-247">[T_THEME_COLOR_NAVIGATION]</span></span>  <br/> |
|<span data-ttu-id="36030-248">NavigationAccent</span><span class="sxs-lookup"><span data-stu-id="36030-248">NavigationAccent</span></span>  <br/> |<span data-ttu-id="36030-249">Textfarbe für ein ausgewähltes horizontales Navigationselement</span><span class="sxs-lookup"><span data-stu-id="36030-249">Text color for a selected horizontal navigation item.</span></span>  <br/> |<span data-ttu-id="36030-250">[T_THEME_COLOR_NAVIGATIONACCENT]</span><span class="sxs-lookup"><span data-stu-id="36030-250">[T_THEME_COLOR_NAVIGATIONACCENT]</span></span>  <br/> |
|<span data-ttu-id="36030-251">NavigationHover</span><span class="sxs-lookup"><span data-stu-id="36030-251">NavigationHover</span></span>  <br/> |<span data-ttu-id="36030-p114">Navigationstextfarbe beim Daraufzeigen. Gilt für obere Navigationselemente und für Schnellstartelemente im horizontalen Modus</span><span class="sxs-lookup"><span data-stu-id="36030-p114">Navigation text color on hover. Applies to top navigation, and to Quick Launch in horizontal mode.</span></span>  <br/> |<span data-ttu-id="36030-254">[T_THEME_COLOR_NAVIGATIONHOVER]</span><span class="sxs-lookup"><span data-stu-id="36030-254">[T_THEME_COLOR_NAVIGATIONHOVER]</span></span>  <br/> |
|<span data-ttu-id="36030-255">NavigationPressed</span><span class="sxs-lookup"><span data-stu-id="36030-255">NavigationPressed</span></span>  <br/> |<span data-ttu-id="36030-p115">Textfarbe von Navigationselementen, wenn diese gedrückt werden. Gilt für obere Navigationselemente und für Schnellstartelemente im horizontalen Modus</span><span class="sxs-lookup"><span data-stu-id="36030-p115">Text color of navigation item when pressed. Applies to top navigation, and to Quick Launch in horizontal mode.</span></span>  <br/> |<span data-ttu-id="36030-258">[T_THEME_COLOR_NAVIGATIONPRESSED]</span><span class="sxs-lookup"><span data-stu-id="36030-258">[T_THEME_COLOR_NAVIGATIONPRESSED]</span></span>  <br/> |
|<span data-ttu-id="36030-259">NavigationHoverBackground</span><span class="sxs-lookup"><span data-stu-id="36030-259">NavigationHoverBackground</span></span>  <br/> |<span data-ttu-id="36030-260">Hintergrundfarbe für Schnellstartelemente im vertikalen Modus beim Daraufzeigen</span><span class="sxs-lookup"><span data-stu-id="36030-260">Background color of Quick Launch items in vertical mode on hover over the navigation item.</span></span>  <br/> |<span data-ttu-id="36030-261">[T_THEME_COLOR_NAVIGATIONHOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-261">[T_THEME_COLOR_NAVIGATIONHOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-262">NavigationSelectedBackground</span><span class="sxs-lookup"><span data-stu-id="36030-262">NavigationSelectedBackground</span></span>  <br/> |<span data-ttu-id="36030-263">Hintergrundfarbe von Schnellstartelementen im vertikalen Modus, nachdem das Navigationselement ausgewählt wurde</span><span class="sxs-lookup"><span data-stu-id="36030-263">Background color of Quick Launch items in vertical mode after the navigation item is selected.</span></span>  <br/> |<span data-ttu-id="36030-264">[T_THEME_COLOR_NAVIGATIONSELECTEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-264">[T_THEME_COLOR_NAVIGATIONSELECTEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-265">EmphasisText</span><span class="sxs-lookup"><span data-stu-id="36030-265">EmphasisText</span></span>  <br/> |<span data-ttu-id="36030-266">Die Textfarbe, die auf hervorgehobenem Hintergrund angezeigt wird</span><span class="sxs-lookup"><span data-stu-id="36030-266">The text color that appears on top of emphasis background.</span></span>  <br/> |<span data-ttu-id="36030-267">[T_THEME_COLOR_EMPHASISTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-267">[T_THEME_COLOR_EMPHASISTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-268">EmphasisBackground</span><span class="sxs-lookup"><span data-stu-id="36030-268">EmphasisBackground</span></span>  <br/> |<span data-ttu-id="36030-269">Die Farbe für hervorgehobenen Hintergrund, der direkt hinter hervorgehobenem Text angezeigt wird</span><span class="sxs-lookup"><span data-stu-id="36030-269">The accented background color that appears directly behind emphasis text.</span></span>  <br/> |<span data-ttu-id="36030-270">[T_THEME_COLOR_EMPHASISBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-270">[T_THEME_COLOR_EMPHASISBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-271">EmphasisHoverBackground</span><span class="sxs-lookup"><span data-stu-id="36030-271">EmphasisHoverBackground</span></span>  <br/> |<span data-ttu-id="36030-272">Hintergrundfarbe beim Daraufzeigen, für Elemente, die hervorgehobenen Hintergrund verwenden</span><span class="sxs-lookup"><span data-stu-id="36030-272">Background color on hover, for elements that are using emphasis background.</span></span>  <br/> |<span data-ttu-id="36030-273">[T_THEME_COLOR_EMPHASISHOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-273">[T_THEME_COLOR_EMPHASISHOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-274">EmphasisBorder</span><span class="sxs-lookup"><span data-stu-id="36030-274">EmphasisBorder</span></span>  <br/> |<span data-ttu-id="36030-275">Rahmenfarbe für Elemente mit hervorgehobenem Hintergrund</span><span class="sxs-lookup"><span data-stu-id="36030-275">Border color for elements that are using emphasis background.</span></span>  <br/> |<span data-ttu-id="36030-276">[T_THEME_COLOR_EMPHASISBORDER]</span><span class="sxs-lookup"><span data-stu-id="36030-276">[T_THEME_COLOR_EMPHASISBORDER]</span></span>  <br/> |
|<span data-ttu-id="36030-277">EmphasisHoverBorder</span><span class="sxs-lookup"><span data-stu-id="36030-277">EmphasisHoverBorder</span></span>  <br/> |<span data-ttu-id="36030-278">Rahmenfarbe beim Daraufzeigen für Elemente mit hervorgehobenem Hintergrund</span><span class="sxs-lookup"><span data-stu-id="36030-278">Border color on hover for elements that are using emphasis background.</span></span>  <br/> |<span data-ttu-id="36030-279">[T_THEME_COLOR_EMPHASISHOVERBORDER]</span><span class="sxs-lookup"><span data-stu-id="36030-279">[T_THEME_COLOR_EMPHASISHOVERBORDER]</span></span>  <br/> |
|<span data-ttu-id="36030-280">SubtleEmphasisText</span><span class="sxs-lookup"><span data-stu-id="36030-280">SubtleEmphasisText</span></span>  <br/> |<span data-ttu-id="36030-281">Text, der auf dezent hervorgehobenem Hintergrund angezeigt wird</span><span class="sxs-lookup"><span data-stu-id="36030-281">Text that appears on top of subtle emphasis background.</span></span>  <br/> |<span data-ttu-id="36030-282">[T_THEME_COLOR_SUBTLEEMPHASISTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-282">[T_THEME_COLOR_SUBTLEEMPHASISTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-283">SubtleEmphasisCommandLinks</span><span class="sxs-lookup"><span data-stu-id="36030-283">SubtleEmphasisCommandLinks</span></span>  <br/> |<span data-ttu-id="36030-284">Befehlslinkfarbe für Links, die auf dezent hervorgehobenem Hintergrund angezeigt werden</span><span class="sxs-lookup"><span data-stu-id="36030-284">Command link color for links that appear on top of subtle emphasis background.</span></span>  <br/> |<span data-ttu-id="36030-285">[T_THEME_COLOR_SUBTLEEMPHASISCOMMANDLINKS]</span><span class="sxs-lookup"><span data-stu-id="36030-285">[T_THEME_COLOR_SUBTLEEMPHASISCOMMANDLINKS]</span></span>  <br/> |
|<span data-ttu-id="36030-286">SubtleEmphasisBackground</span><span class="sxs-lookup"><span data-stu-id="36030-286">SubtleEmphasisBackground</span></span>  <br/> |<span data-ttu-id="36030-287">Hintergrund, der direkt hinter dezent hervorgehobenem Text angezeigt wird</span><span class="sxs-lookup"><span data-stu-id="36030-287">Background that appears directly behind subtle emphasis text.</span></span>  <br/> |<span data-ttu-id="36030-288">[T_THEME_COLOR_SUBTLEEMPHASISBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-288">[T_THEME_COLOR_SUBTLEEMPHASISBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-289">TopBarText</span><span class="sxs-lookup"><span data-stu-id="36030-289">TopBarText</span></span>  <br/> |<span data-ttu-id="36030-290">Text- und Glyphenfarbe für das Willkommensmenü, Symbole auf der Schnellzugriffsleiste und geschlossene Registerkarten auf dem Menüband</span><span class="sxs-lookup"><span data-stu-id="36030-290">Text and glyph color for the welcome menu, quick access toolbar icons, and closed ribbon tabs.</span></span>  <br/> |<span data-ttu-id="36030-291">[T_THEME_COLOR_TOPBARTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-291">[T_THEME_COLOR_TOPBARTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-292">TopBarBackground</span><span class="sxs-lookup"><span data-stu-id="36030-292">TopBarBackground</span></span>  <br/> |<span data-ttu-id="36030-293">Die Hintergrundfarbe für die obere Leiste, die unterhalb und rechts der Suitenavigation angezeigt wird</span><span class="sxs-lookup"><span data-stu-id="36030-293">The background color for the top bar, which is seen below and to the right of the suite navigation.</span></span>  <br/> |<span data-ttu-id="36030-294">[T_THEME_COLOR_TOPBARBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-294">[T_THEME_COLOR_TOPBARBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-295">TopBarHoverText</span><span class="sxs-lookup"><span data-stu-id="36030-295">TopBarHoverText</span></span>  <br/> |<span data-ttu-id="36030-296">Text- und Glyphenfarbe beim Daraufzeigen für das Willkommensmenü, Symbole auf der Schnellzugriffsleiste und geschlossene Registerkarten auf dem Menüband</span><span class="sxs-lookup"><span data-stu-id="36030-296">Text and glyph color on hover for the welcome menu, quick access toolbar icons, and closed ribbon tabs.</span></span>  <br/> |<span data-ttu-id="36030-297">[T_THEME_COLOR_TOPBARHOVERTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-297">[T_THEME_COLOR_TOPBARHOVERTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-298">TopBarPressedText</span><span class="sxs-lookup"><span data-stu-id="36030-298">TopBarPressedText</span></span>  <br/> |<span data-ttu-id="36030-299">Text- und Glyphenfarbe beim Drücken auf das Willkommensmenü, Symbole auf der Schnellzugriffsleiste und geschlossene Registerkarten auf dem Menüband</span><span class="sxs-lookup"><span data-stu-id="36030-299">Text and glyph color for when the welcome menu, quick access toolbar icons, or closed ribbon tabs are pressed.</span></span>  <br/> |<span data-ttu-id="36030-300">[T_THEME_COLOR_TOPBARPRESSEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-300">[T_THEME_COLOR_TOPBARPRESSEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-301">HeaderText</span><span class="sxs-lookup"><span data-stu-id="36030-301">HeaderText</span></span>  <br/> |<span data-ttu-id="36030-302">Die Basistextfarbe für den gesamten Kopfbereich</span><span class="sxs-lookup"><span data-stu-id="36030-302">The base text color for anything in the header area.</span></span>  <br/> |<span data-ttu-id="36030-303">[T_THEME_COLOR_HEADERTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-303">[T_THEME_COLOR_HEADERTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-304">HeaderSubtleText</span><span class="sxs-lookup"><span data-stu-id="36030-304">HeaderSubtleText</span></span>  <br/> |<span data-ttu-id="36030-305">Hilfetext für das Suchfeld im Kopfbereich</span><span class="sxs-lookup"><span data-stu-id="36030-305">Helper text for the search box when in the header area.</span></span>  <br/> |<span data-ttu-id="36030-306">[T_THEME_COLOR_HEADERSUBTLETEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-306">[T_THEME_COLOR_HEADERSUBTLETEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-307">HeaderDisableText</span><span class="sxs-lookup"><span data-stu-id="36030-307">HeaderDisableText</span></span>  <br/> |<span data-ttu-id="36030-308">Text für das Suchfeld, wenn sich das Suchfeld im Kopfbereich befindet und deaktiviert ist</span><span class="sxs-lookup"><span data-stu-id="36030-308">Text for the search box, if the search box is disabled when in the header area.</span></span>  <br/> |<span data-ttu-id="36030-309">[T_THEME_COLOR_HEADERDISABLETEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-309">[T_THEME_COLOR_HEADERDISABLETEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-310">HeaderNavigationText</span><span class="sxs-lookup"><span data-stu-id="36030-310">HeaderNavigationText</span></span>  <br/> |<span data-ttu-id="36030-311">Basistextfarbe für Navigationslinks im Kopfbereich</span><span class="sxs-lookup"><span data-stu-id="36030-311">Base text color for navigation links in the header area.</span></span>  <br/> |<span data-ttu-id="36030-312">[T_THEME_COLOR_HEADERNAVIGATIONTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-312">[T_THEME_COLOR_HEADERNAVIGATIONTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-313">HeaderNavigationHoverText</span><span class="sxs-lookup"><span data-stu-id="36030-313">HeaderNavigationHoverText</span></span>  <br/> |<span data-ttu-id="36030-314">Textfarbe für Navigationslinks im Kopfbereich beim Daraufzeigen auf den Link</span><span class="sxs-lookup"><span data-stu-id="36030-314">Text color for navigation links in the header area when you hover over the link.</span></span>  <br/> |<span data-ttu-id="36030-315">[T_THEME_COLOR_HEADERNAVIGATIONHOVERTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-315">[T_THEME_COLOR_HEADERNAVIGATIONHOVERTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-316">HeaderNavigationPressedText</span><span class="sxs-lookup"><span data-stu-id="36030-316">HeaderNavigationPressedText</span></span>  <br/> |<span data-ttu-id="36030-317">Textfarbe für Navigationlinks im Kopfbereich beim Drücken des Links</span><span class="sxs-lookup"><span data-stu-id="36030-317">Text color for navigation links in the header area when you press the link.</span></span>  <br/> |<span data-ttu-id="36030-318">[T_THEME_COLOR_HEADERNAVIGATIONPRESSEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-318">[T_THEME_COLOR_HEADERNAVIGATIONPRESSEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-319">HeaderNavigationSelectedText</span><span class="sxs-lookup"><span data-stu-id="36030-319">HeaderNavigationSelectedText</span></span>  <br/> |<span data-ttu-id="36030-320">Textfarbe für Navigationslinks im Kopfbereich bei Auswahl des Links</span><span class="sxs-lookup"><span data-stu-id="36030-320">Text color for navigation links in the header area after the link is selected.</span></span>  <br/> |<span data-ttu-id="36030-321">[T_THEME_COLOR_HEADERNAVIGATIONSELECTEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-321">[T_THEME_COLOR_HEADERNAVIGATIONSELECTEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-322">HeaderLines</span><span class="sxs-lookup"><span data-stu-id="36030-322">HeaderLines</span></span>  <br/> |<span data-ttu-id="36030-323">Suchfeldlinien, wenn sich das Suchfeld im Kopfbereich befindet</span><span class="sxs-lookup"><span data-stu-id="36030-323">Search box lines when the search box is in the header area.</span></span>  <br/> |<span data-ttu-id="36030-324">[T_THEME_COLOR_HEADERLINES]</span><span class="sxs-lookup"><span data-stu-id="36030-324">[T_THEME_COLOR_HEADERLINES]</span></span>  <br/> |
|<span data-ttu-id="36030-325">HeaderStrongLines</span><span class="sxs-lookup"><span data-stu-id="36030-325">HeaderStrongLines</span></span>  <br/> |<span data-ttu-id="36030-326">Suchfeldlinien beim Daraufzeigen, wenn sich das Suchfeld im Kopfbereich befindet</span><span class="sxs-lookup"><span data-stu-id="36030-326">Search box lines on hover when the search box is in the header area.</span></span>  <br/> |<span data-ttu-id="36030-327">[T_THEME_COLOR_HEADERSTRONGLINES]</span><span class="sxs-lookup"><span data-stu-id="36030-327">[T_THEME_COLOR_HEADERSTRONGLINES]</span></span>  <br/> |
|<span data-ttu-id="36030-328">HeaderAccentLines</span><span class="sxs-lookup"><span data-stu-id="36030-328">HeaderAccentLines</span></span>  <br/> |<span data-ttu-id="36030-329">Suchfeldlinien im Fokus, wenn sich das Suchfeld im Kopfbereich befindet</span><span class="sxs-lookup"><span data-stu-id="36030-329">Search box lines on focus when the search box is in the header area.</span></span>  <br/> |<span data-ttu-id="36030-330">[T_THEME_COLOR_HEADERACCENTLINES]</span><span class="sxs-lookup"><span data-stu-id="36030-330">[T_THEME_COLOR_HEADERACCENTLINES]</span></span>  <br/> |
|<span data-ttu-id="36030-331">HeaderSublteLines</span><span class="sxs-lookup"><span data-stu-id="36030-331">HeaderSublteLines</span></span>  <br/> |<span data-ttu-id="36030-p116">Dezente Linien im Kopfbereich. Werden in CSS-Standarddateien nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="36030-p116">Subtle lines found inside the header area. Not used in default CSS.</span></span>  <br/> |<span data-ttu-id="36030-334">[T_THEME_COLOR_HEADERSUBTLELINES]</span><span class="sxs-lookup"><span data-stu-id="36030-334">[T_THEME_COLOR_HEADERSUBTLELINES]</span></span>  <br/> |
|<span data-ttu-id="36030-335">HeaderDisabledLines</span><span class="sxs-lookup"><span data-stu-id="36030-335">HeaderDisabledLines</span></span>  <br/> |<span data-ttu-id="36030-336">Suchfeldlinien, wenn sich das Suchfeld im Kopfbereich befindet und deaktiviert ist</span><span class="sxs-lookup"><span data-stu-id="36030-336">Search box lines if the search box is disabled when it's in the header area.</span></span>  <br/> |<span data-ttu-id="36030-337">[T_THEME_COLOR_HEADERDISABLEDLINES]</span><span class="sxs-lookup"><span data-stu-id="36030-337">[T_THEME_COLOR_HEADERDISABLEDLINES]</span></span>  <br/> |
|<span data-ttu-id="36030-338">HeaderDisabledBackground</span><span class="sxs-lookup"><span data-stu-id="36030-338">HeaderDisabledBackground</span></span>  <br/> |<span data-ttu-id="36030-339">Suchfeldhintergrund, wenn sich das Suchfeld im Kopfbereich befindet und deaktiviert ist</span><span class="sxs-lookup"><span data-stu-id="36030-339">Search box background if the search box is disabled when it's in the header area.</span></span>  <br/> |<span data-ttu-id="36030-340">[T_THEME_COLOR_HEADERDISABLEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-340">[T_THEME_COLOR_HEADERDISABLEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-341">HeaderFlyoutBorder</span><span class="sxs-lookup"><span data-stu-id="36030-341">HeaderFlyoutBorder</span></span>  <br/> |<span data-ttu-id="36030-342">Rahmen für Dropdownmenüs im Kopfbereich</span><span class="sxs-lookup"><span data-stu-id="36030-342">Border for drop-down menus when originating from the header area.</span></span>  <br/> |<span data-ttu-id="36030-343">[T_THEME_COLOR_HEADERFLYOUTBORDER]</span><span class="sxs-lookup"><span data-stu-id="36030-343">[T_THEME_COLOR_HEADERFLYOUTBORDER]</span></span>  <br/> |
|<span data-ttu-id="36030-344">HeaderSiteTitle</span><span class="sxs-lookup"><span data-stu-id="36030-344">HeaderSiteTitle</span></span>  <br/> |<span data-ttu-id="36030-345">Textfarbe für den Websitetitel im Kopfbereich</span><span class="sxs-lookup"><span data-stu-id="36030-345">Text color for the site title when in the header area.</span></span>  <br/> |<span data-ttu-id="36030-346">[T_THEME_COLOR_HEADERSITETITLE]</span><span class="sxs-lookup"><span data-stu-id="36030-346">[T_THEME_COLOR_HEADERSITETITLE]</span></span>  <br/> |
|<span data-ttu-id="36030-347">SuiteBarBackground</span><span class="sxs-lookup"><span data-stu-id="36030-347">SuiteBarBackground</span></span>  <br/> |<span data-ttu-id="36030-348">Hintergrundfarbe für die Suitenavigation</span><span class="sxs-lookup"><span data-stu-id="36030-348">Background color for the suite navigation.</span></span>  <br/> |<span data-ttu-id="36030-349">[T_THEME_COLOR_SUITEBARBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-349">[T_THEME_COLOR_SUITEBARBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-350">SuiteBarHoverBackground</span><span class="sxs-lookup"><span data-stu-id="36030-350">SuiteBarHoverBackground</span></span>  <br/> |<span data-ttu-id="36030-351">Hintergrundfarbe beim Daraufzeigen für die Suitenavigation</span><span class="sxs-lookup"><span data-stu-id="36030-351">Background color on hover for the suite navigation.</span></span>  <br/> |<span data-ttu-id="36030-352">[T_THEME_COLOR_SUITEBARHOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-352">[T_THEME_COLOR_SUITEBARHOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-353">SuiteBarText</span><span class="sxs-lookup"><span data-stu-id="36030-353">SuiteBarText</span></span>  <br/> |<span data-ttu-id="36030-354">Text- und Glyphenfarbe für die Suitenavigationselemente</span><span class="sxs-lookup"><span data-stu-id="36030-354">Text and glyph color for the suite navigation items.</span></span>  <br/> |<span data-ttu-id="36030-355">[T_THEME_COLOR_SUITEBARTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-355">[T_THEME_COLOR_SUITEBARTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-356">SuiteBarDisabledText</span><span class="sxs-lookup"><span data-stu-id="36030-356">SuiteBarDisabledText</span></span>  <br/> |<span data-ttu-id="36030-p117">Text- und Glyphenfarbe für deaktivierte Suiteelemente. Wird in CSS-Standarddateien nicht verwendet.</span><span class="sxs-lookup"><span data-stu-id="36030-p117">Text and glyph color for disabled suite items. Not used in default CSS.</span></span>  <br/> |<span data-ttu-id="36030-359">[T_THEME_COLOR_SUITEBARDISABLEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-359">[T_THEME_COLOR_SUITEBARDISABLEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-360">ButtonText</span><span class="sxs-lookup"><span data-stu-id="36030-360">ButtonText</span></span>  <br/> |<span data-ttu-id="36030-361">Textfarbe für Schaltflächen</span><span class="sxs-lookup"><span data-stu-id="36030-361">Text color for buttons.</span></span>  <br/> |<span data-ttu-id="36030-362">[T_THEME_COLOR_BUTTONTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-362">[T_THEME_COLOR_BUTTONTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-363">ButtonDisabledText</span><span class="sxs-lookup"><span data-stu-id="36030-363">ButtonDisabledText</span></span>  <br/> |<span data-ttu-id="36030-364">Textfarbe für deaktivierte Schaltflächen</span><span class="sxs-lookup"><span data-stu-id="36030-364">Text color for disabled buttons.</span></span>  <br/> |<span data-ttu-id="36030-365">[T_THEME_COLOR_BUTTONDISABLEDTEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-365">[T_THEME_COLOR_BUTTONDISABLEDTEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-366">ButtonBackground</span><span class="sxs-lookup"><span data-stu-id="36030-366">ButtonBackground</span></span>  <br/> |<span data-ttu-id="36030-367">Hintergrundfarbe für Schaltflächen</span><span class="sxs-lookup"><span data-stu-id="36030-367">Background color for buttons.</span></span>  <br/> |<span data-ttu-id="36030-368">[T_THEME_COLOR_BUTTONBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-368">[T_THEME_COLOR_BUTTONBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-369">ButtonHoverBackground</span><span class="sxs-lookup"><span data-stu-id="36030-369">ButtonHoverBackground</span></span>  <br/> |<span data-ttu-id="36030-370">Hintergrundfarbe für Schaltflächen beim Daraufzeigen</span><span class="sxs-lookup"><span data-stu-id="36030-370">Background color for buttons on hover.</span></span>  <br/> |<span data-ttu-id="36030-371">[T_THEME_COLOR_BUTTONHOVERBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-371">[T_THEME_COLOR_BUTTONHOVERBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-372">ButtonPressedBackground</span><span class="sxs-lookup"><span data-stu-id="36030-372">ButtonPressedBackground</span></span>  <br/> |<span data-ttu-id="36030-373">Hintergrundfarbe für gedrückte Schaltflächen</span><span class="sxs-lookup"><span data-stu-id="36030-373">Background color for buttons while pressed.</span></span>  <br/> |<span data-ttu-id="36030-374">[T_THEME_COLOR_BUTTONPRESSEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-374">[T_THEME_COLOR_BUTTONPRESSEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-375">ButtonDisabledBackground</span><span class="sxs-lookup"><span data-stu-id="36030-375">ButtonDisabledBackground</span></span>  <br/> |<span data-ttu-id="36030-376">Hintergrundfarbe für deaktivierte Schaltflächen</span><span class="sxs-lookup"><span data-stu-id="36030-376">Background color for disabled buttons.</span></span>  <br/> |<span data-ttu-id="36030-377">[T_THEME_COLOR_BUTTONDISABLEDBACKGROUND]</span><span class="sxs-lookup"><span data-stu-id="36030-377">[T_THEME_COLOR_BUTTONDISABLEDBACKGROUND]</span></span>  <br/> |
|<span data-ttu-id="36030-378">ButtonBorder</span><span class="sxs-lookup"><span data-stu-id="36030-378">ButtonBorder</span></span>  <br/> |<span data-ttu-id="36030-379">Rahmenfarbe für Schaltflächen</span><span class="sxs-lookup"><span data-stu-id="36030-379">Border color for buttons.</span></span>  <br/> |<span data-ttu-id="36030-380">[T_THEME_COLOR_BUTTONBORDER]</span><span class="sxs-lookup"><span data-stu-id="36030-380">[T_THEME_COLOR_BUTTONBORDER]</span></span>  <br/> |
|<span data-ttu-id="36030-381">ButtonHoverBorder</span><span class="sxs-lookup"><span data-stu-id="36030-381">ButtonHoverBorder</span></span>  <br/> |<span data-ttu-id="36030-382">Rahmenfarbe für Schaltflächen beim Daraufzeigen</span><span class="sxs-lookup"><span data-stu-id="36030-382">Border color for buttons on hover.</span></span>  <br/> |<span data-ttu-id="36030-383">[T_THEME_COLOR_BUTTONHOVERBORDER]</span><span class="sxs-lookup"><span data-stu-id="36030-383">[T_THEME_COLOR_BUTTONHOVERBORDER]</span></span>  <br/> |
|<span data-ttu-id="36030-384">ButtonPressedBorder</span><span class="sxs-lookup"><span data-stu-id="36030-384">ButtonPressedBorder</span></span>  <br/> |<span data-ttu-id="36030-385">Rahmenfarbe für gedrückte Schaltflächen</span><span class="sxs-lookup"><span data-stu-id="36030-385">Border color for buttons while pressed.</span></span>  <br/> |<span data-ttu-id="36030-386">[T_THEME_COLOR_BUTTONPRESSEDBORDER]</span><span class="sxs-lookup"><span data-stu-id="36030-386">[T_THEME_COLOR_BUTTONPRESSEDBORDER]</span></span>  <br/> |
|<span data-ttu-id="36030-387">ButtonDisabledBorder</span><span class="sxs-lookup"><span data-stu-id="36030-387">ButtonDisabledBorder</span></span>  <br/> |<span data-ttu-id="36030-388">Rahmenfarbe für Schaltflächen, die deaktiviert sind</span><span class="sxs-lookup"><span data-stu-id="36030-388">Border color for buttons that are disabled.</span></span>  <br/> |<span data-ttu-id="36030-389">[T_THEME_COLOR_BUTTONDISABLEDBORDER]</span><span class="sxs-lookup"><span data-stu-id="36030-389">[T_THEME_COLOR_BUTTONDISABLEDBORDER]</span></span>  <br/> |
|<span data-ttu-id="36030-390">ButtonGlyph</span><span class="sxs-lookup"><span data-stu-id="36030-390">ButtonGlyph</span></span>  <br/> |<span data-ttu-id="36030-391">Glyphenfarbe für eine Glyphe, die in einer Schaltfläche angezeigt wird</span><span class="sxs-lookup"><span data-stu-id="36030-391">Glyph color for a glyph that appears in a button.</span></span>  <br/> |<span data-ttu-id="36030-392">[T_THEME_COLOR_BUTTONGLYPH]</span><span class="sxs-lookup"><span data-stu-id="36030-392">[T_THEME_COLOR_BUTTONGLYPH]</span></span>  <br/> |
|<span data-ttu-id="36030-393">ButtonGlyphActive</span><span class="sxs-lookup"><span data-stu-id="36030-393">ButtonGlyphActive</span></span>  <br/> |<span data-ttu-id="36030-394">Glyphenfarbe beim Daraufzeigen, für eine Glyphe, die in einer Schaltfläche angezeigt wird</span><span class="sxs-lookup"><span data-stu-id="36030-394">Glyph color on hover, for a glyph that appears in a button.</span></span>  <br/> |<span data-ttu-id="36030-395">[T_THEME_COLOR_BUTTONGLYPHACTIVE]</span><span class="sxs-lookup"><span data-stu-id="36030-395">[T_THEME_COLOR_BUTTONGLYPHACTIVE]</span></span>  <br/> |
|<span data-ttu-id="36030-396">ButtonGlyphDisabled</span><span class="sxs-lookup"><span data-stu-id="36030-396">ButtonGlyphDisabled</span></span>  <br/> |<span data-ttu-id="36030-397">Glyphenfarbe für eine deaktivierte Schaltfläche</span><span class="sxs-lookup"><span data-stu-id="36030-397">Glyph color for a disabled button.</span></span>  <br/> |<span data-ttu-id="36030-398">[T_THEME_COLOR_BUTTONGLYPHDISABLED]</span><span class="sxs-lookup"><span data-stu-id="36030-398">[T_THEME_COLOR_BUTTONGLYPHDISABLED]</span></span>  <br/> |
|<span data-ttu-id="36030-399">TileText</span><span class="sxs-lookup"><span data-stu-id="36030-399">TileText</span></span>  <br/> |<span data-ttu-id="36030-400">Der Text, der auf überlagertem Kachelhintergrund angezeigt wird</span><span class="sxs-lookup"><span data-stu-id="36030-400">The text that appears on top of the tile background overlay.</span></span>  <br/> |<span data-ttu-id="36030-401">[T_THEME_COLOR_TILETEXT]</span><span class="sxs-lookup"><span data-stu-id="36030-401">[T_THEME_COLOR_TILETEXT]</span></span>  <br/> |
|<span data-ttu-id="36030-402">TileBackgroundOverlay</span><span class="sxs-lookup"><span data-stu-id="36030-402">TileBackgroundOverlay</span></span>  <br/> |<span data-ttu-id="36030-403">Die Hintergrundüberlagerungsfarbe für Kacheln</span><span class="sxs-lookup"><span data-stu-id="36030-403">The background overlay color for tiles.</span></span>  <br/> |<span data-ttu-id="36030-404">[T_THEME_COLOR_TILEBACKGROUNDOVERLAY]</span><span class="sxs-lookup"><span data-stu-id="36030-404">[T_THEME_COLOR_TILEBACKGROUNDOVERLAY]</span></span>  <br/> |
|<span data-ttu-id="36030-405">ContentAccent1</span><span class="sxs-lookup"><span data-stu-id="36030-405">ContentAccent1</span></span>  <br/> |<span data-ttu-id="36030-406">Die erste Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann</span><span class="sxs-lookup"><span data-stu-id="36030-406">The first accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="36030-407">[T_THEME_COLOR_CONTENTACCENT1]</span><span class="sxs-lookup"><span data-stu-id="36030-407">[T_THEME_COLOR_CONTENTACCENT1]</span></span>  <br/> |
|<span data-ttu-id="36030-408">ContentAccent2</span><span class="sxs-lookup"><span data-stu-id="36030-408">ContentAccent2</span></span>  <br/> |<span data-ttu-id="36030-409">Die zweite Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann</span><span class="sxs-lookup"><span data-stu-id="36030-409">The second accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="36030-410">[T_THEME_COLOR_CONTENTACCENT2]</span><span class="sxs-lookup"><span data-stu-id="36030-410">[T_THEME_COLOR_CONTENTACCENT2]</span></span>  <br/> |
|<span data-ttu-id="36030-411">ContentAccent3</span><span class="sxs-lookup"><span data-stu-id="36030-411">ContentAccent3</span></span>  <br/> |<span data-ttu-id="36030-412">Die dritte Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann</span><span class="sxs-lookup"><span data-stu-id="36030-412">The third accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="36030-413">[T_THEME_COLOR_CONTENTACCENT3]</span><span class="sxs-lookup"><span data-stu-id="36030-413">[T_THEME_COLOR_CONTENTACCENT3]</span></span>  <br/> |
|<span data-ttu-id="36030-414">ContentAccent4</span><span class="sxs-lookup"><span data-stu-id="36030-414">ContentAccent4</span></span>  <br/> |<span data-ttu-id="36030-415">Die vierte Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann</span><span class="sxs-lookup"><span data-stu-id="36030-415">The fourth accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="36030-416">[T_THEME_COLOR_CONTENTACCENT4]</span><span class="sxs-lookup"><span data-stu-id="36030-416">[T_THEME_COLOR_CONTENTACCENT4]</span></span>  <br/> |
|<span data-ttu-id="36030-417">ContentAccent5</span><span class="sxs-lookup"><span data-stu-id="36030-417">ContentAccent5</span></span>  <br/> |<span data-ttu-id="36030-418">Die fünfte Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann</span><span class="sxs-lookup"><span data-stu-id="36030-418">The fifth accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="36030-419">[T_THEME_COLOR_CONTENTACCENT5]</span><span class="sxs-lookup"><span data-stu-id="36030-419">[T_THEME_COLOR_CONTENTACCENT5]</span></span>  <br/> |
|<span data-ttu-id="36030-420">ContentAccent6</span><span class="sxs-lookup"><span data-stu-id="36030-420">ContentAccent6</span></span>  <br/> |<span data-ttu-id="36030-421">Die sechste Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann</span><span class="sxs-lookup"><span data-stu-id="36030-421">The sixth accent color that a user can select from the Rich Text Editor color picker.</span></span>  <br/> |<span data-ttu-id="36030-422">[T_THEME_COLOR_CONTENTACCENT6]</span><span class="sxs-lookup"><span data-stu-id="36030-422">[T_THEME_COLOR_CONTENTACCENT6]</span></span>  <br/> |
   

## <a name="font-schemes"></a><span data-ttu-id="36030-423">Schriftartenschema</span><span class="sxs-lookup"><span data-stu-id="36030-423">Font schemes</span></span>
<span data-ttu-id="36030-424"><a name="font"> </a></span><span class="sxs-lookup"><span data-stu-id="36030-424"><a name="font"> </a></span></span>

<span data-ttu-id="36030-p118">Schriftarten werden im Schriftartenschema (.spfont-Datei) und der Gestaltungsvorlagenvorschau (.preview-Datei) für eine bestimmte SharePoint-Website definiert. Das Schriftartenschema definiert die Schriftarten, die in vier Bereichen verwendet werden: Titel, Navigation, Überschrift und Textkörper. Sieben Schriftartenschemas sind in SharePoint enthalten. Sie können zusätzliche Schriftartenschemas erstellen. Die Schriftartenschemadateien sind im **15**-Unterordner des Designkatalogs der Stammwebsite der Websitesammlung abgelegt (http:// _SiteCollectionName_/_catalogs/theme/15/). Um den Designkatalog über die Benutzerfläche von SharePoint aufzurufen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** **Designs** und dann **15** aus.</span><span class="sxs-lookup"><span data-stu-id="36030-p118">Fonts are defined in the font scheme (.spfont file) and the master page preview (.preview file) for a given SharePoint site. The font scheme defines the fonts that are used in four areas: title, navigation, heading, and body. Seven font schemes are included in SharePoint. You can create additional font schemes. The font scheme files are located in the **15** subfolder of the Theme Gallery of the root site of the site collection (http:// _SiteCollectionName_/_catalogs/theme/15/). To access the Theme Gallery from the SharePoint user interface, on the **Site Settings** page, under **Web Designer Galleries**, select **Themes**, and then select **15**.</span></span>
  
    
    
<span data-ttu-id="36030-431">Das folgende Beispiel beschreibt das Format für eine .spfont-Datei.</span><span class="sxs-lookup"><span data-stu-id="36030-431">The following example describes the format for an .spfont file.</span></span>
  
    
    



```xml

<?xml version="1.0" encoding="utf-8"?>
<s:fontScheme name="FontSchemeName" previewSlot1="Slot1" previewSlot2="Slot2" xmlns:s="http://schemas.microsoft.com/sharepoint/">
  <s:fontSlots>
    <s:fontSlot name="FontSlotName">
      <s:latin typeface="LatinScriptFont" />
      <s:ea typeface="EAScriptFont"/>
      <s:cs typeface="CSFont" />
      <s:font script="Language" typeface="ScriptFont" />
      <!--Additional fonts-->
  </s:fontSlots>
  <!--Additional font slots-->
</s:fontScheme>
```

<span data-ttu-id="36030-432">In einer .spfont-Datei werden die folgenden Platzhalter ersetzt:</span><span class="sxs-lookup"><span data-stu-id="36030-432">In an .spfont file, the following placeholders are replaced:</span></span>
  
    
    

-  <span data-ttu-id="36030-433">_FontSchemeName_ ist der Name des Schriftartenschemas.</span><span class="sxs-lookup"><span data-stu-id="36030-433">_FontSchemeName_ is the name of the font scheme.</span></span>
    
  
-  <span data-ttu-id="36030-434">_Slot1_ ist der Name des Schriftartenplatzes, den Sie als den ersten Block des Schriftartensymbols in der Schriftartenschemaauswahl im Assistenten **Aussehen ändern** verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="36030-434">_Slot1_ is the name of the font slot that you want to use as the first block of the font icon in the font scheme picker in the **Change the look** wizard.</span></span>
    
  
-  <span data-ttu-id="36030-435">_Slot2_ ist der Name des Schriftartenplatzes, den Sie als den zweiten Block des Schriftartensymbols in der Schriftartenschemaauswahl im Assistenten **Aussehen ändern** verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="36030-435">_Slot2_ is the name of the font slot that you want to use as the second block of the font icon in the font scheme picker in the **Change the look** wizard.</span></span>
    
  
-  <span data-ttu-id="36030-436">_FontSlotName_ ist der Name des Schriftartenplatzes, den Sie definieren (z. B. Titel).</span><span class="sxs-lookup"><span data-stu-id="36030-436">_FontSlotName_ is the name of the font slot that you are defining (for example, title).</span></span>
    
  
-  <span data-ttu-id="36030-p119">_LatinScriptFont_ ist die Schriftart, die für lateinische Skripts verwendet werden soll. Diese Schriftart ist ebenfalls die Fallbackschriftart. Das bedeutet, dass diese Schriftart für eine Sprache verwendet wird, die kein im Schriftartenschema explizit festgelegtes Skript aufweist.</span><span class="sxs-lookup"><span data-stu-id="36030-p119">_LatinScriptFont_ is the font to use for Latin scripts. This font is also the fallback font. That is, this is the font that is used for a language that does not have a script that is explicitly set in the font scheme.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="36030-440">Sie müssen zusätzliche Informationen bereitstellen, wenn Sie Webschriftarten in Ihrem Schriftartenschema verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="36030-440">Note: You must provide additional information to use web fonts in your font scheme.</span></span> <span data-ttu-id="36030-441">Weitere Informationen finden Sie im Abschnitt [Webschriftarten](#webFont) dieses Artikels.</span><span class="sxs-lookup"><span data-stu-id="36030-441">For more information, see the  [Web fonts](#webFont) section in this article.</span></span>
-  <span data-ttu-id="36030-p121">_EAScriptFont_ ist die Schriftart, die für ostasiatische Skripts verwendet werden soll. Das **<s:ea>**-Element wird von SharePoint derzeit nicht verwendet. Das **<s:ea>**-Element wird im Schriftartenschema dennoch benötigt.</span><span class="sxs-lookup"><span data-stu-id="36030-p121">_EAScriptFont_ is the font to use for East Asia scripts. The **<s:ea>** element is not currently used by SharePoint. But, the **<s:ea>** element is still required in the font scheme.</span></span>
    
  
-  <span data-ttu-id="36030-p122">_CSFont_ ist die Schriftart, die für komplexe Skripts verwendet werden soll. Das **<s:cs>**-Element wird von SharePoint derzeit nicht verwendet. Das **<s:cs>**-Element wird im Schriftartenschema dennoch benötigt.</span><span class="sxs-lookup"><span data-stu-id="36030-p122">_CSFont_ is the font to use for complex scripts. The **<s:cs>** element is not currently used by SharePoint. But, the **<s:cs>** element is still required in the font scheme.</span></span>
    
  
-  <span data-ttu-id="36030-448">_Language_ ist das Sprachenskript.</span><span class="sxs-lookup"><span data-stu-id="36030-448">_Language_ is the language script.</span></span>
    
  
-  <span data-ttu-id="36030-449">_ScriptFont_ ist die Schriftart, die für das angegebene Sprachenskript verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="36030-449">_ScriptFont_ is the font to use for the specified language script.</span></span>
    
  
<span data-ttu-id="36030-450">Das folgende Beispiel zeigt einen Teil einer .spfont-Datei.</span><span class="sxs-lookup"><span data-stu-id="36030-450">The following example shows a portion of an .spfont file.</span></span>
  
    
    



```xml

<s:fontScheme name="Georgia" previewSlot1="title" previewSlot2="body" xmlns:s="http://schemas.microsoft.com/sharepoint/">
    <s:fontSlots>
        <s:fontSlot name="title">
            <s:latin typeface="Georgia"/>
            <s:ea typeface=""/>
            <s:cs typeface="Segoe UI Light" />
            <s:font script="Arab" typeface="Tahoma" />
            <s:font script="Deva" typeface="Mangal" />
            <s:font script="Grek" typeface="Segoe UI Light" />
            <s:font script="Hang" typeface="Malgun Gothic" />
            <s:font script="Hans" typeface="Microsoft YaHei" />
            <s:font script="Hant" typeface="Microsoft JhengHei" />
            <s:font script="Hebr" typeface="Tahoma" />
            <s:font script="Hira" typeface="Meiryo" />
            <s:font script="Thai" typeface="Tahoma" />
            <s:font script="Armn" typeface="Tahoma" />
            <s:font script="Beng" typeface="Vrinda" />
            <s:font script="Cher" typeface="Plantagenet Cherokee" />
            <s:font script="Ethi" typeface="Nyala" />
            <s:font script="Geor" typeface="Sylfaen" />
            <s:font script="Gujr" typeface="Shruti" />
            <s:font script="Guru" typeface="Raavi" />
            <s:font script="Knda" typeface="Tunga" />
            <s:font script="Khmr" typeface="DaunPenh" />
            <s:font script="Laoo" typeface="DokChampa" />
            <s:font script="Mlym" typeface="Kartika" />
            <s:font script="Mymr" typeface="Myanmar Text" />
            <s:font script="Orya" typeface="Kalinga" />
            <s:font script="Sinh" typeface="Iskoola Pota" />
            <s:font script="Syrc" typeface="Estrangelo Edessa" />
            <s:font script="Taml" typeface="Latha" />
            <s:font script="Telu" typeface="Gautami" />
            <s:font script="Thaa" typeface="MV Boli" />
            <s:font script="Tibt" typeface="Cordia New" />
            <s:font script="Yiii" typeface="Microsoft Yi Baiti" />
        </s:fontSlot>
???
```

<span data-ttu-id="36030-p123">SharePoint umfasst Unterstützung für Webschriftarten. Sie müssen zusätzliche Informationen angeben, um in Ihrem Schriftartenschema Webschriftarten zu verwenden. Weitere Informationen finden Sie unter in diesem Artikel im Abschnitt  [Webschriftarten](#webFont).</span><span class="sxs-lookup"><span data-stu-id="36030-p123">SharePoint includes support for web fonts. You must provide additional information to use web fonts in your font scheme. For more information, see the  [Web fonts](#webFont) section in this article.</span></span>
  
    
    

### <a name="web-safe-fonts"></a><span data-ttu-id="36030-454">Websichere Schriftarten</span><span class="sxs-lookup"><span data-stu-id="36030-454">Web-safe fonts</span></span>
<span data-ttu-id="36030-455"><a name="websafeFont"> </a></span><span class="sxs-lookup"><span data-stu-id="36030-455"><a name="websafeFont"> </a></span></span>

<span data-ttu-id="36030-p124">Als websichere Schriftarten werden Schriftarten bezeichnet, die häufig verwendet werden und auf den meisten Geräten standardmäßig verfügbar sind. Um im Schriftartenschema eine websichere Schriftart anzugeben, schließen Sie den Namen der Schriftart in das **typeface**-Attribut des Schriftartenplatzes ein. Das folgende Beispiel zeigt eine websichere Schriftart, die in einem Schriftartenschema verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="36030-p124">Web-safe fonts are a set of fonts that are widely used and available on most devices by default. To specify a web-safe font in the font scheme, include the name of the font in the **typeface** attribute of the font slot. The following example shows a web-safe font used in a font scheme.</span></span>
  
    
    

```xml

<s:fontSlot name="title">
  <s:latin typeface="Georgia"/>
???
</s:fontSlot>
```


### <a name="web-fonts"></a><span data-ttu-id="36030-459">Webschriftarten</span><span class="sxs-lookup"><span data-stu-id="36030-459">Web fonts</span></span>
<span data-ttu-id="36030-460"><a name="webFont"> </a></span><span class="sxs-lookup"><span data-stu-id="36030-460"><a name="webFont"> </a></span></span>

<span data-ttu-id="36030-p125">Webschriftarten sind Schriftarten, die im Internet verfügbar sind. Wenn ein Benutzer eine Website anzeigt, die Webschriftarten verwendet, lädt der Webbrowser mit der restlichen Seite die erforderlichen Schriftartendateien herunter. Um eine Webschriftart anzugeben, müssen Sie die URL zu Ihren Webschriftartendateien in vier Schriftartenformaten angeben (für browserübergreifende Unterstützung) sowie ein kleines und ein großes Miniaturbild, mit dem die Schriftartennamen in der Schriftartenschemaauswahl wiedergegeben werden.</span><span class="sxs-lookup"><span data-stu-id="36030-p125">Web fonts are fonts that are available on the Internet. When a user views a site that uses web fonts, the web browser downloads the necessary font files along with the rest of the page. To specify a web font, you must provide the URL to your web font files in four font formats (for support across browsers), and a small and large thumbnail image to use to render the font names in the font scheme picker.</span></span>
  
    
    
<span data-ttu-id="36030-464">Das folgende Beispiel beschreibt die Informationen, die erforderlich sind, um eine Webschriftart in einem **<s:latin>**-Element zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="36030-464">The following example describes the information that is required to use a web font in an **<s:latin>** element.</span></span>
  
    
    



```xml

<s:latin typeface="FontName"
  eotsrc="EotFile"
  woffsrc="WoffFile"
  ttfsrc="TtfFile"
  svgsrc="SvgFile"
  largeimgsrc="LargeImgFile"
  smallimgsrc="SmallImgFile" />

```

<span data-ttu-id="36030-465">In diesem Beispiel für die Verwendung einer Webschriftart würden die folgenden Platzhalter ersetzt werden:</span><span class="sxs-lookup"><span data-stu-id="36030-465">In this example of using a web font, the following placeholders would be replaced:</span></span>
  
    
    

-  <span data-ttu-id="36030-466">_FontName_ ist der Name der Webschriftart.</span><span class="sxs-lookup"><span data-stu-id="36030-466">_FontName_ is the name of the web font.</span></span>
    
  
-  <span data-ttu-id="36030-467">_EotFile_ ist die relative URL zur Embedded OpenType-Schriftartendatei.</span><span class="sxs-lookup"><span data-stu-id="36030-467">_EotFile_ is the relative URL to the Embedded Open Type font file.</span></span>
    
  
-  <span data-ttu-id="36030-468">_WoffFile_ ist die relative URL zur Web Open Font Format-Schriftartendatei.</span><span class="sxs-lookup"><span data-stu-id="36030-468">_WoffFile_ is the relative URL to the Web Open Font Format font file.</span></span>
    
  
-  <span data-ttu-id="36030-469">_TtfFile_ ist die relative URL zur TrueType-Schriftartendatei.</span><span class="sxs-lookup"><span data-stu-id="36030-469">_TtfFile_ is the relative URL to the TrueType font file.</span></span>
    
  
-  <span data-ttu-id="36030-470">_SvgFile_ ist die relative URL zur Scalable Vector Graphics-Schriftartendatei.</span><span class="sxs-lookup"><span data-stu-id="36030-470">_SvgFile_ is the relative URL to the Scalable Vector Graphics font file.</span></span>
    
  
-  <span data-ttu-id="36030-471">_LargeImgFile_ ist die relative URL zum großen Miniaturbild, das Sie in der Schriftartenschemaauswahl verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="36030-471">_LargeImgFile_ is the relative URL to the large thumbnail image that you want to use in the font scheme picker.</span></span>
    
  
-  <span data-ttu-id="36030-472">_SmallImgFile_ ist die relative URL zum kleinen Miniaturbild, das Sie in der Schriftartenschemaauswahl verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="36030-472">_SmallImgFile_ is the relative URL to the small thumbnail image that you want to use in the font scheme picker.</span></span>
    
  

### <a name="font-slots"></a><span data-ttu-id="36030-473">Schriftartenplätze</span><span class="sxs-lookup"><span data-stu-id="36030-473">Font slots</span></span>
<span data-ttu-id="36030-474"><a name="fontSlot"> </a></span><span class="sxs-lookup"><span data-stu-id="36030-474"><a name="fontSlot"> </a></span></span>

<span data-ttu-id="36030-475">Tabelle 1 beschreibt die verfügbaren Schriftartenplätze und die Stellen, an denen sie in einer Seite verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="36030-475">Table 1 describes the available font slots and where they are used in a page.</span></span>
  
    
    

<span data-ttu-id="36030-476">**Tabelle 1. Schriftartenplätze**</span><span class="sxs-lookup"><span data-stu-id="36030-476">**Table 1. Font slots**</span></span>


|<span data-ttu-id="36030-477">**Name des Schriftartenplatzes**</span><span class="sxs-lookup"><span data-stu-id="36030-477">**Font Slot Name**</span></span>|<span data-ttu-id="36030-478">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="36030-478">**Description**</span></span>|
|:-----|:-----|
|<span data-ttu-id="36030-479">title</span><span class="sxs-lookup"><span data-stu-id="36030-479">title</span></span>  <br/> |<span data-ttu-id="36030-480">Wird für den Seitentitel verwendet</span><span class="sxs-lookup"><span data-stu-id="36030-480">Used for the page title.</span></span>  <br/> |
|<span data-ttu-id="36030-481">Navigation</span><span class="sxs-lookup"><span data-stu-id="36030-481">navigation</span></span>  <br/> |<span data-ttu-id="36030-482">Wird für die horizontalen und vertikalen Navigationselemente auf der Seite verwendet</span><span class="sxs-lookup"><span data-stu-id="36030-482">Used for the horizontal and vertical navigation elements on the page.</span></span>  <br/> |
|<span data-ttu-id="36030-483">large-heading</span><span class="sxs-lookup"><span data-stu-id="36030-483">large-heading</span></span>  <br/> |<span data-ttu-id="36030-484">Wird für die H1-Überschrift verwendet</span><span class="sxs-lookup"><span data-stu-id="36030-484">Used for the H1 heading.</span></span>  <br/> |
|<span data-ttu-id="36030-485">heading</span><span class="sxs-lookup"><span data-stu-id="36030-485">heading</span></span>  <br/> |<span data-ttu-id="36030-486">Wird für H2- und H3-Überschriften, Webpart-Titel, Dialogfeldtitel und Popuptitel verwendet</span><span class="sxs-lookup"><span data-stu-id="36030-486">Used for H2 and H3 headings, Web Part titles, dialog box titles, and callout titles.</span></span>  <br/> |
|<span data-ttu-id="36030-487">small-heading</span><span class="sxs-lookup"><span data-stu-id="36030-487">small-heading</span></span>  <br/> |<span data-ttu-id="36030-488">Wird für H4-Überschriften verwendet</span><span class="sxs-lookup"><span data-stu-id="36030-488">Used for H4 headings.</span></span>  <br/> |
|<span data-ttu-id="36030-489">large-body</span><span class="sxs-lookup"><span data-stu-id="36030-489">large-body</span></span>  <br/> |<span data-ttu-id="36030-490">Wird für großen Fließtext verwendet (15 Pixel und 19 Pixel)</span><span class="sxs-lookup"><span data-stu-id="36030-490">Used for large body text (15 pixels and 19 pixels).</span></span>  <br/> |
|<span data-ttu-id="36030-491">body</span><span class="sxs-lookup"><span data-stu-id="36030-491">body</span></span>  <br/> |<span data-ttu-id="36030-492">Die Basisschriftart, die an allen anderen Stellen auf der Seite verwendet wird</span><span class="sxs-lookup"><span data-stu-id="36030-492">The base font that is used everywhere else on the page.</span></span>  <br/> |
   

## <a name="see-also"></a><span data-ttu-id="36030-493">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="36030-493">See also</span></span>
<span data-ttu-id="36030-494"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="36030-494"><a name="bk_addresources"> </a></span></span>


-  [<span data-ttu-id="36030-495">Übersicht über Designs für SharePoint</span><span class="sxs-lookup"><span data-stu-id="36030-495">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md)
    
  
-  [<span data-ttu-id="36030-496">Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="36030-496">How to: Deploy a custom theme in SharePoint</span></span>](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [<span data-ttu-id="36030-497">Aktualisieren benutzerdefinierter Designs und CSS-Dateien auf SharePoint</span><span class="sxs-lookup"><span data-stu-id="36030-497">Upgrade custom themes and CSS to SharePoint</span></span>](upgrade-custom-themes-and-css-to-sharepoint.md)
    
  
-  [<span data-ttu-id="36030-498">Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint</span><span class="sxs-lookup"><span data-stu-id="36030-498">How to: Create a master page preview file in SharePoint</span></span>](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [<span data-ttu-id="36030-499">SharePoint-Teamblog: Beweisen Sie Stil mit SharePoint-Designs</span><span class="sxs-lookup"><span data-stu-id="36030-499">SharePoint Team Blog: Show off your style with SharePoint theming</span></span>](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [<span data-ttu-id="36030-500">SharePoint Design Manager - Branding- und Designfunktionen</span><span class="sxs-lookup"><span data-stu-id="36030-500">SharePoint Design Manager branding and design capabilities</span></span>](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

  
    
    

