---
title: Use composed looks to brand SharePoint sites
ms.date: 11/03/2017
ms.openlocfilehash: a3c9450690227785cb368f09a299fc769168ce89
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-composed-looks-to-brand-sharepoint-sites"></a><span data-ttu-id="89522-102">Use composed looks to brand SharePoint sites</span><span class="sxs-lookup"><span data-stu-id="89522-102">Use composed looks to brand SharePoint sites</span></span>

<span data-ttu-id="89522-103">Apply composed looks, including colors, fonts, and a background image, to your SharePoint 2013 and SharePoint Online sites by using the SharePoint theming engine.</span><span class="sxs-lookup"><span data-stu-id="89522-103">Apply composed looks, including colors, fonts, and a background image, to your SharePoint 2013 and SharePoint Online sites by using the SharePoint theming engine.</span></span>

<span data-ttu-id="89522-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="89522-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="89522-105">You can apply composed looks to your SharePoint sites.</span><span class="sxs-lookup"><span data-stu-id="89522-105">You can apply composed looks to your SharePoint sites.</span></span> <span data-ttu-id="89522-106">Composed looks are out-of-the-box themes that are included in SharePoint 2013 and SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="89522-106">Composed looks are out-of-the-box themes that are included in SharePoint 2013 and SharePoint Online.</span></span> <span data-ttu-id="89522-107">To apply a composed look to a SharePoint site, select **Site Settings** > **Look and Feel** > **Change the look**.</span><span class="sxs-lookup"><span data-stu-id="89522-107">To apply a composed look to a SharePoint site, select **Site Settings** > **Look and Feel** > **Change the look**.</span></span> <span data-ttu-id="89522-108">You can then use the Change the look wizard to customize the colors, fonts, master page, and background image of a composed look.</span><span class="sxs-lookup"><span data-stu-id="89522-108">You can then use the Change the look wizard to customize the colors, fonts, master page, and background image of a composed look.</span></span> <span data-ttu-id="89522-109">The Change the look wizard copies, transforms, and stores CSS in SharePoint's content database.</span><span class="sxs-lookup"><span data-stu-id="89522-109">The Change the look wizard copies, transforms, and stores CSS in SharePoint's content database.</span></span> <span data-ttu-id="89522-110">It also recolors images and stores them in the content database.</span><span class="sxs-lookup"><span data-stu-id="89522-110">It also recolors images and stores them in the content database.</span></span> 

## <a name="sharepoint-theming-engine"></a><span data-ttu-id="89522-111">SharePoint theming engine</span><span class="sxs-lookup"><span data-stu-id="89522-111">SharePoint theming engine</span></span>
<span data-ttu-id="89522-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="89522-112"></span></span>

<span data-ttu-id="89522-113">You can use the SharePoint 2013 theming engine to apply colors, fonts, and a background image to a site by associating those elements with a master page.</span><span class="sxs-lookup"><span data-stu-id="89522-113">You can use the SharePoint 2013 theming engine to apply colors, fonts, and a background image to a site by associating those elements with a master page.</span></span>

<span data-ttu-id="89522-114">In SharePoint 2013 and SharePoint Online, a theme is a connected set of XML definition files, an image file, and an associated master page that you can use to apply custom CSS to a site.</span><span class="sxs-lookup"><span data-stu-id="89522-114">In SharePoint 2013 and SharePoint Online, a theme is a connected set of XML definition files, an image file, and an associated master page that you can use to apply custom CSS to a site.</span></span> <span data-ttu-id="89522-115">The following XML files define color slots and font slots that define the details of specific colors and fonts as they're applied to styles:</span><span class="sxs-lookup"><span data-stu-id="89522-115">The following XML files define color slots and font slots that define the details of specific colors and fonts as they're applied to styles:</span></span> 

- <span data-ttu-id="89522-116">.spcolor</span><span class="sxs-lookup"><span data-stu-id="89522-116">.spcolor</span></span>
    
- <span data-ttu-id="89522-117">.spfont</span><span class="sxs-lookup"><span data-stu-id="89522-117">.spfont</span></span>
    
<span data-ttu-id="89522-118">You can create your own color and font files in your favorite text editor.</span><span class="sxs-lookup"><span data-stu-id="89522-118">You can create your own color and font files in your favorite text editor.</span></span>

<span data-ttu-id="89522-119">The following table lists the elements of a composed look.</span><span class="sxs-lookup"><span data-stu-id="89522-119">The following table lists the elements of a composed look.</span></span>

|<span data-ttu-id="89522-120">**Element**</span><span class="sxs-lookup"><span data-stu-id="89522-120">**Element**</span></span>|<span data-ttu-id="89522-121">**File or files**</span><span class="sxs-lookup"><span data-stu-id="89522-121">**File or files**</span></span>|<span data-ttu-id="89522-122">**Where it's stored**</span><span class="sxs-lookup"><span data-stu-id="89522-122">**Where it's stored**</span></span>|<span data-ttu-id="89522-123">**Erforderlich?**</span><span class="sxs-lookup"><span data-stu-id="89522-123">**Required?**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="89522-124">Farbpalette</span><span class="sxs-lookup"><span data-stu-id="89522-124">Color palette</span></span>|<span data-ttu-id="89522-125">.spcolor</span><span class="sxs-lookup"><span data-stu-id="89522-125">.spcolor</span></span>|<span data-ttu-id="89522-126">Theme Gallery\15 folder</span><span class="sxs-lookup"><span data-stu-id="89522-126">Theme Gallery\15 folder</span></span>|<span data-ttu-id="89522-127">Ja</span><span class="sxs-lookup"><span data-stu-id="89522-127">Yes</span></span>|
|<span data-ttu-id="89522-128">Font scheme</span><span class="sxs-lookup"><span data-stu-id="89522-128">Font scheme</span></span>|<span data-ttu-id="89522-129">.spfont</span><span class="sxs-lookup"><span data-stu-id="89522-129">.spfont</span></span>|<span data-ttu-id="89522-130">Theme Gallery\15 folder</span><span class="sxs-lookup"><span data-stu-id="89522-130">Theme Gallery\15 folder</span></span>|<span data-ttu-id="89522-131">Nein</span><span class="sxs-lookup"><span data-stu-id="89522-131">No</span></span>|
|<span data-ttu-id="89522-132">Site layout</span><span class="sxs-lookup"><span data-stu-id="89522-132">Site layout</span></span>|<p><span data-ttu-id="89522-133">.master</span><span class="sxs-lookup"><span data-stu-id="89522-133">.master</span></span></p><p><span data-ttu-id="89522-134">.preview</span><span class="sxs-lookup"><span data-stu-id="89522-134">.preview</span></span></p>|<span data-ttu-id="89522-135">Master Page Gallery</span><span class="sxs-lookup"><span data-stu-id="89522-135">Master Page Gallery</span></span>|<span data-ttu-id="89522-136">Ja</span><span class="sxs-lookup"><span data-stu-id="89522-136">Yes</span></span>|
|<span data-ttu-id="89522-137">Background image</span><span class="sxs-lookup"><span data-stu-id="89522-137">Background image</span></span>|<p><span data-ttu-id="89522-138">.jpg</span><span class="sxs-lookup"><span data-stu-id="89522-138">.jpg</span></span></p><p><span data-ttu-id="89522-139">.bmp</span><span class="sxs-lookup"><span data-stu-id="89522-139">.bmp</span></span></p><p><span data-ttu-id="89522-140">.png</span><span class="sxs-lookup"><span data-stu-id="89522-140">.png</span></span></p><p><span data-ttu-id="89522-141">.gif</span><span class="sxs-lookup"><span data-stu-id="89522-141">.gif</span></span></p>|<span data-ttu-id="89522-142">Site assets</span><span class="sxs-lookup"><span data-stu-id="89522-142">Site assets</span></span>|<span data-ttu-id="89522-143">Nein</span><span class="sxs-lookup"><span data-stu-id="89522-143">No</span></span>|
<span data-ttu-id="89522-144">Users can select composed looks by using the Change the look wizard (**Site Settings** > **Look and Feel** > **Change the Look**), the Getting Started UI, or directly in the site actions menu.</span><span class="sxs-lookup"><span data-stu-id="89522-144">Users can select composed looks by using the Change the look wizard (**Site Settings** > **Look and Feel** > **Change the Look**), the Getting Started UI, or directly in the site actions menu.</span></span> <span data-ttu-id="89522-145">When a user selects a composed look, the theming engine applies colors, fonts, background images, the associated .master page, and the .preview file associated with the .master page to the site.</span><span class="sxs-lookup"><span data-stu-id="89522-145">When a user selects a composed look, the theming engine applies colors, fonts, background images, the associated .master page, and the .preview file associated with the .master page to the site.</span></span> 

### <a name="color-palettes"></a><span data-ttu-id="89522-146">Color palettes</span><span class="sxs-lookup"><span data-stu-id="89522-146">Color palettes</span></span>

<span data-ttu-id="89522-147">The theming engine stores colors in color palettes defined by the .spcolor file, as shown in Figure 1.</span><span class="sxs-lookup"><span data-stu-id="89522-147">The theming engine stores colors in color palettes defined by the .spcolor file, as shown in Figure 1.</span></span> <span data-ttu-id="89522-148">Color palettes are stored in the Theme Gallery of the root site.</span><span class="sxs-lookup"><span data-stu-id="89522-148">Color palettes are stored in the Theme Gallery of the root site.</span></span> <span data-ttu-id="89522-149">A color palette is an editable XML file made up of color palette definitions and color slots.</span><span class="sxs-lookup"><span data-stu-id="89522-149">A color palette is an editable XML file made up of color palette definitions and color slots.</span></span> <span data-ttu-id="89522-150">Color palette metadata ( `<s:colorPalette>`) defines the following:</span><span class="sxs-lookup"><span data-stu-id="89522-150">Color palette metadata ( `<s:colorPalette>`) defines the following:</span></span>

- <span data-ttu-id="89522-151">Three preview slots that define what color slots to use in composed look previews.</span><span class="sxs-lookup"><span data-stu-id="89522-151">Three preview slots that define what color slots to use in composed look previews.</span></span>
    
- <span data-ttu-id="89522-152">An  **isInverted** property that lets the palette designer specify whether the theme is inverted (dark background with light text).</span><span class="sxs-lookup"><span data-stu-id="89522-152">An  **isInverted** property that lets the palette designer specify whether the theme is inverted (dark background with light text).</span></span>
    
- <span data-ttu-id="89522-153">The XML namespace associated with the theme.</span><span class="sxs-lookup"><span data-stu-id="89522-153">The XML namespace associated with the theme.</span></span>
    
<span data-ttu-id="89522-154">Color slots are defined by two attributesâ€”color name and valueâ€”that define a name for the color and its RGB value.</span><span class="sxs-lookup"><span data-stu-id="89522-154">Color slots are defined by two attributesâ€”color name and valueâ€”that define a name for the color and its RGB value.</span></span> <span data-ttu-id="89522-155">Color slots have semantic names, such as BodyText or SiteTitle, that help you identify which slots correspond to a region of a SharePoint page.</span><span class="sxs-lookup"><span data-stu-id="89522-155">Color slots have semantic names, such as BodyText or SiteTitle, that help you identify which slots correspond to a region of a SharePoint page.</span></span>

`<s:color name="BodyText" value="444444" />`

<span data-ttu-id="89522-156">**Figure 1. .spcolor file**</span><span class="sxs-lookup"><span data-stu-id="89522-156">**Figure 1. .spcolor file**</span></span>

![Screenshot of an .spcolor file showing color name and value attributes](media/16de0716-2e21-471f-b9e5-f461a33b397b.png)

<span data-ttu-id="89522-158">Line 2 of the .spcolor file defines the XML namespace, preview slots, and whether colors are inverted (they have a light foreground on a dark background instead of a dark foreground on a light background).</span><span class="sxs-lookup"><span data-stu-id="89522-158">Line 2 of the .spcolor file defines the XML namespace, preview slots, and whether colors are inverted (they have a light foreground on a dark background instead of a dark foreground on a light background).</span></span> 

<span data-ttu-id="89522-159">The .spcolor file contains 89 color slots.</span><span class="sxs-lookup"><span data-stu-id="89522-159">The .spcolor file contains 89 color slots.</span></span> <span data-ttu-id="89522-160">You can use color slots to define richer aspects of color, including opacity, by using 8-digit hexadecimal values.</span><span class="sxs-lookup"><span data-stu-id="89522-160">You can use color slots to define richer aspects of color, including opacity, by using 8-digit hexadecimal values.</span></span> <span data-ttu-id="89522-161">For example, if green is RRGGBB 00FF00, a 70 percent opaque green is AARRGGBB 7F00FF00.</span><span class="sxs-lookup"><span data-stu-id="89522-161">For example, if green is RRGGBB 00FF00, a 70 percent opaque green is AARRGGBB 7F00FF00.</span></span> <span data-ttu-id="89522-162">If SharePoint uses a slot that you don't define, any CSS that references it won't change color.</span><span class="sxs-lookup"><span data-stu-id="89522-162">If SharePoint uses a slot that you don't define, any CSS that references it won't change color.</span></span> <span data-ttu-id="89522-163">If a slot is defined that is never referenced in CSS, the color is never shown in the UI.</span><span class="sxs-lookup"><span data-stu-id="89522-163">If a slot is defined that is never referenced in CSS, the color is never shown in the UI.</span></span>

<span data-ttu-id="89522-164">You can edit the .spcolor file in Notepad.</span><span class="sxs-lookup"><span data-stu-id="89522-164">You can edit the .spcolor file in Notepad.</span></span> <span data-ttu-id="89522-165">You cannot edit it in PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="89522-165">You cannot edit it in PowerPoint.</span></span>

### <a name="color-palette-tool"></a><span data-ttu-id="89522-166">Color palette tool</span><span class="sxs-lookup"><span data-stu-id="89522-166">Color palette tool</span></span>

<span data-ttu-id="89522-167">You can use the  [color palette tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) to visualize theme colors and how they work together on the page.</span><span class="sxs-lookup"><span data-stu-id="89522-167">You can use the  [color palette tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) to visualize theme colors and how they work together on the page.</span></span> <span data-ttu-id="89522-168">Use it to identify color information you can use in the color slots of the .spcolor file, and apply colors to a SharePoint site without changing any CSS as part of the process.</span><span class="sxs-lookup"><span data-stu-id="89522-168">Use it to identify color information you can use in the color slots of the .spcolor file, and apply colors to a SharePoint site without changing any CSS as part of the process.</span></span>

<span data-ttu-id="89522-169">The tool displays the colors in hexadecimal format, so you can easily copy and paste the color value into the appropriate element in your .spcolor file.</span><span class="sxs-lookup"><span data-stu-id="89522-169">The tool displays the colors in hexadecimal format, so you can easily copy and paste the color value into the appropriate element in your .spcolor file.</span></span> <span data-ttu-id="89522-170">You can also use the color palette tool to fit a background image into a mockup and toggle between the seattle.master and oslo.master master pages.</span><span class="sxs-lookup"><span data-stu-id="89522-170">You can also use the color palette tool to fit a background image into a mockup and toggle between the seattle.master and oslo.master master pages.</span></span> 


<span data-ttu-id="89522-171">**Figure 2. Color palette tool**</span><span class="sxs-lookup"><span data-stu-id="89522-171">**Figure 2. Color palette tool**</span></span>

![Screenshot of the color palette tool](media/407d8095-20cd-4d9b-be53-493d95b4653c.png)

<span data-ttu-id="89522-173">The .spcolor file is the only file that is required for a new theme, but you might need to add some custom font declarations, depending on the depth of your design.</span><span class="sxs-lookup"><span data-stu-id="89522-173">The .spcolor file is the only file that is required for a new theme, but you might need to add some custom font declarations, depending on the depth of your design.</span></span> <span data-ttu-id="89522-174">To do that, you need to access the .spfont file.</span><span class="sxs-lookup"><span data-stu-id="89522-174">To do that, you need to access the .spfont file.</span></span>

### <a name="font-schemes"></a><span data-ttu-id="89522-175">Font schemes</span><span class="sxs-lookup"><span data-stu-id="89522-175">Font schemes</span></span>

<span data-ttu-id="89522-176">In the same way that color palettes define how colors are used in composed looks, font schemes define the fonts in composed looks.</span><span class="sxs-lookup"><span data-stu-id="89522-176">In the same way that color palettes define how colors are used in composed looks, font schemes define the fonts in composed looks.</span></span> 

<span data-ttu-id="89522-177">Font schemes are defined in the .spfont file stored in the Theme Gallery.</span><span class="sxs-lookup"><span data-stu-id="89522-177">Font schemes are defined in the .spfont file stored in the Theme Gallery.</span></span> <span data-ttu-id="89522-178">The .spfont file includes the following font slots that define the name, typeface, and script values of a composed look:</span><span class="sxs-lookup"><span data-stu-id="89522-178">The .spfont file includes the following font slots that define the name, typeface, and script values of a composed look:</span></span>

- <span data-ttu-id="89522-179">Titel</span><span class="sxs-lookup"><span data-stu-id="89522-179">Title</span></span>
    
- <span data-ttu-id="89522-180">Navigation</span><span class="sxs-lookup"><span data-stu-id="89522-180">Navigation</span></span>
    
- <span data-ttu-id="89522-181">Small-heading</span><span class="sxs-lookup"><span data-stu-id="89522-181">Small-heading</span></span>
    
- <span data-ttu-id="89522-182">Heading</span><span class="sxs-lookup"><span data-stu-id="89522-182">Heading</span></span>
    
- <span data-ttu-id="89522-183">Large-heading</span><span class="sxs-lookup"><span data-stu-id="89522-183">Large-heading</span></span>
    
- <span data-ttu-id="89522-184">Body</span><span class="sxs-lookup"><span data-stu-id="89522-184">Body</span></span>
    
- <span data-ttu-id="89522-185">Large-body</span><span class="sxs-lookup"><span data-stu-id="89522-185">Large-body</span></span>
    
<span data-ttu-id="89522-186">Fonts are further scoped by script type (for example, Latin, Arabic, Cyrillic).</span><span class="sxs-lookup"><span data-stu-id="89522-186">Fonts are further scoped by script type (for example, Latin, Arabic, Cyrillic).</span></span> <span data-ttu-id="89522-187">Web fonts support is included in four file types:</span><span class="sxs-lookup"><span data-stu-id="89522-187">Web fonts support is included in four file types:</span></span>

- <span data-ttu-id="89522-188">Embedded open type (EOT)</span><span class="sxs-lookup"><span data-stu-id="89522-188">Embedded open type (EOT)</span></span>
    
- <span data-ttu-id="89522-189">Web open font format file (WOFF)</span><span class="sxs-lookup"><span data-stu-id="89522-189">Web open font format file (WOFF)</span></span>
    
- <span data-ttu-id="89522-190">TrueType font (TTF)</span><span class="sxs-lookup"><span data-stu-id="89522-190">TrueType font (TTF)</span></span>
    
- <span data-ttu-id="89522-191">Scalable vector graphics (SVG)</span><span class="sxs-lookup"><span data-stu-id="89522-191">Scalable vector graphics (SVG)</span></span>
    
<span data-ttu-id="89522-192">The font scheme defines a large preview image and a small preview image.</span><span class="sxs-lookup"><span data-stu-id="89522-192">The font scheme defines a large preview image and a small preview image.</span></span> <span data-ttu-id="89522-193">They are required only for web fonts.</span><span class="sxs-lookup"><span data-stu-id="89522-193">They are required only for web fonts.</span></span>

> [!NOTE] 
> <span data-ttu-id="89522-194">You can edit the .spfont file in Notepad.</span><span class="sxs-lookup"><span data-stu-id="89522-194">You can edit the .spfont file in Notepad.</span></span> <span data-ttu-id="89522-195">You cannot edit it in PowerPoint.</span><span class="sxs-lookup"><span data-stu-id="89522-195">You cannot edit it in PowerPoint.</span></span>

<span data-ttu-id="89522-196">The following is an example of an .spfont file.</span><span class="sxs-lookup"><span data-stu-id="89522-196">The following is an example of an .spfont file.</span></span>

```XML
<?xml version="1.0" encoding="utf-8"?>
<s:fontScheme name="Georgia" previewSlot1="title" previewSlot2="body"
  xmlns:s=http://schemas.microsoft.com/sharepoint/>
    <s:fontSlots>
        <s:fontSlot name="title">
            <s:latin typeface="Georgia"/>
            <s:font script="Arab" typeface="Calibri" />
            <s:font script="Deva" typeface="Mangal" />
            . . . 
        </s:fontSlot>
    <s:fontSlot name="navigation">
        <s:latin typeface="Georgia"/>
        <s:font script="Arab" typeface="Calibri" />
        <s:font script="Deva" typeface="Mangal" />
        . . . 
        </s:fontSlot>
    </s:fontSlots>
</s:fontScheme>
```

### <a name="site-layout-master-pages-and-corresponding-preview-files"></a><span data-ttu-id="89522-197">Site layout: master pages and corresponding preview files</span><span class="sxs-lookup"><span data-stu-id="89522-197">Site layout: master pages and corresponding preview files</span></span>

<span data-ttu-id="89522-198">The theming engine defines the site layout of a composed look based on the .master master page and its corresponding .preview file.</span><span class="sxs-lookup"><span data-stu-id="89522-198">The theming engine defines the site layout of a composed look based on the .master master page and its corresponding .preview file.</span></span> <span data-ttu-id="89522-199">For example, if the master page defined for the composed look is seattle.master, that master page defines the layout of the site.</span><span class="sxs-lookup"><span data-stu-id="89522-199">For example, if the master page defined for the composed look is seattle.master, that master page defines the layout of the site.</span></span>

<span data-ttu-id="89522-200">The site layout is pulled from the Master Page Gallery of any master pages that have accompanying .preview files.</span><span class="sxs-lookup"><span data-stu-id="89522-200">The site layout is pulled from the Master Page Gallery of any master pages that have accompanying .preview files.</span></span> <span data-ttu-id="89522-201">A .preview file is required for a master page to appear as an option in the **Change the look** UI (**Site Settings** > **Look and Feel** > **Change the look**).</span><span class="sxs-lookup"><span data-stu-id="89522-201">A .preview file is required for a master page to appear as an option in the **Change the look** UI (**Site Settings** > **Look and Feel** > **Change the look**).</span></span>

<span data-ttu-id="89522-202">To make a master page available from the Site Layout drop-down menu, create a .preview file that corresponds to the .master page.</span><span class="sxs-lookup"><span data-stu-id="89522-202">To make a master page available from the Site Layout drop-down menu, create a .preview file that corresponds to the .master page.</span></span> <span data-ttu-id="89522-203">The .preview file displays thumbnail images for the composed look and the preview section to the right of the **Change the look** options on the designbuilder.aspx page.</span><span class="sxs-lookup"><span data-stu-id="89522-203">The .preview file displays thumbnail images for the composed look and the preview section to the right of the **Change the look** options on the designbuilder.aspx page.</span></span>

### <a name="background-image"></a><span data-ttu-id="89522-204">Background image</span><span class="sxs-lookup"><span data-stu-id="89522-204">Background image</span></span>

<span data-ttu-id="89522-205">You can change the background image of a composed look by choosing **Change**.</span><span class="sxs-lookup"><span data-stu-id="89522-205">You can change the background image of a composed look by choosing **Change**.</span></span> <span data-ttu-id="89522-206">This opens an upload dialog box that you can use to upload an image file.</span><span class="sxs-lookup"><span data-stu-id="89522-206">This opens an upload dialog box that you can use to upload an image file.</span></span> <span data-ttu-id="89522-207">You can also drag your own image onto the background preview.</span><span class="sxs-lookup"><span data-stu-id="89522-207">You can also drag your own image onto the background preview.</span></span>

## <a name="create-custom-themes"></a><span data-ttu-id="89522-208">Create custom themes</span><span class="sxs-lookup"><span data-stu-id="89522-208">Create custom themes</span></span>
<span data-ttu-id="89522-209"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="89522-209"></span></span>

<span data-ttu-id="89522-210">To create a custom theme:</span><span class="sxs-lookup"><span data-stu-id="89522-210">To create a custom theme:</span></span>

1. <span data-ttu-id="89522-211">Go to **Site settings**, and under the Web Designer Galleries heading, select **Themes** > **15**.</span><span class="sxs-lookup"><span data-stu-id="89522-211">Go to **Site settings**, and under the Web Designer Galleries heading, select **Themes** > **15**.</span></span> <span data-ttu-id="89522-212">A list of .spcolor and .spfont files appears, as shown in Figure 3.</span><span class="sxs-lookup"><span data-stu-id="89522-212">A list of .spcolor and .spfont files appears, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="89522-213">**Figure 3. Theme Gallery**</span><span class="sxs-lookup"><span data-stu-id="89522-213">**Figure 3. Theme Gallery**</span></span>

    ![Screenshot of the Theme Gallery showing fontscheme and pallette files](media/76e9b4f3-5838-4cd8-9f2f-33a0c94bfddd.png)

2. <span data-ttu-id="89522-215">Download a copy of one of the .spcolor files (for example, Palette001.spcolor) and open it in a text editor.</span><span class="sxs-lookup"><span data-stu-id="89522-215">Download a copy of one of the .spcolor files (for example, Palette001.spcolor) and open it in a text editor.</span></span> 
    
3. <span data-ttu-id="89522-216">Edit the copied .spcolor file to reflect your design guidelines.</span><span class="sxs-lookup"><span data-stu-id="89522-216">Edit the copied .spcolor file to reflect your design guidelines.</span></span> <span data-ttu-id="89522-217">For example, if you have a black font for main body text, edit the file to change the line  `<s:color name="BodyText" value="444444" />` to `<s:color name="BodyText" value="000000" />`.</span><span class="sxs-lookup"><span data-stu-id="89522-217">For example, if you have a black font for main body text, edit the file to change the line  `<s:color name="BodyText" value="444444" />` to `<s:color name="BodyText" value="000000" />`.</span></span>
    
4. <span data-ttu-id="89522-218">For each HTML element, add your color.</span><span class="sxs-lookup"><span data-stu-id="89522-218">For each HTML element, add your color.</span></span> 
    
5. <span data-ttu-id="89522-219">When you are done, upload the .spcolor file to the **Site settings** > **Theme** > **15** folder.</span><span class="sxs-lookup"><span data-stu-id="89522-219">When you are done, upload the .spcolor file to the **Site settings** > **Theme** > **15** folder.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="89522-220">Save the file with a new file name (for example, custom_palette1.spcolor).</span><span class="sxs-lookup"><span data-stu-id="89522-220">Save the file with a new file name (for example, custom_palette1.spcolor).</span></span>

   <span data-ttu-id="89522-221">The following table maps colors and page elements to their code in the .spcolor file.</span><span class="sxs-lookup"><span data-stu-id="89522-221">The following table maps colors and page elements to their code in the .spcolor file.</span></span> <span data-ttu-id="89522-222">It is a subset of the mappings that are available in the .spcolor file.</span><span class="sxs-lookup"><span data-stu-id="89522-222">It is a subset of the mappings that are available in the .spcolor file.</span></span>
    

    |<span data-ttu-id="89522-223">**Element**</span><span class="sxs-lookup"><span data-stu-id="89522-223">**Element**</span></span>|<span data-ttu-id="89522-224">**Farbe**</span><span class="sxs-lookup"><span data-stu-id="89522-224">**Color**</span></span>|<span data-ttu-id="89522-225">**Code**</span><span class="sxs-lookup"><span data-stu-id="89522-225">**Code**</span></span>|
    |:-----|:-----|:-----|
    |<span data-ttu-id="89522-226">Body text</span><span class="sxs-lookup"><span data-stu-id="89522-226">Body text</span></span>|<span data-ttu-id="89522-227">Black</span><span class="sxs-lookup"><span data-stu-id="89522-227">Black</span></span>| `<s:color name="BodyText" value="000000" />`|
    |<span data-ttu-id="89522-228">Global navigation background</span><span class="sxs-lookup"><span data-stu-id="89522-228">Global navigation background</span></span>|<span data-ttu-id="89522-229">Blue</span><span class="sxs-lookup"><span data-stu-id="89522-229">Blue</span></span>| `<s:color name="HeaderBackground" value="018dff" />`|
    |<span data-ttu-id="89522-230">Global navigation text</span><span class="sxs-lookup"><span data-stu-id="89522-230">Global navigation text</span></span>|<span data-ttu-id="89522-231">White</span><span class="sxs-lookup"><span data-stu-id="89522-231">White</span></span>| `<s:color name="HeaderNavigationText" value="ffffff" />`|
    |<span data-ttu-id="89522-232">Current navigation background</span><span class="sxs-lookup"><span data-stu-id="89522-232">Current navigation background</span></span>|<span data-ttu-id="89522-233">Red</span><span class="sxs-lookup"><span data-stu-id="89522-233">Red</span></span>| `<s:color name="NavigationHoverBackground" value="e51400" />`|
    |<span data-ttu-id="89522-234">Current navigation text</span><span class="sxs-lookup"><span data-stu-id="89522-234">Current navigation text</span></span>|<span data-ttu-id="89522-235">White</span><span class="sxs-lookup"><span data-stu-id="89522-235">White</span></span>| `<s:color name="Navigation" value="ffffff" />`|
    |<span data-ttu-id="89522-236">Titel</span><span class="sxs-lookup"><span data-stu-id="89522-236">Title</span></span>|<span data-ttu-id="89522-237">White</span><span class="sxs-lookup"><span data-stu-id="89522-237">White</span></span>| `<s:color name="SiteTitle" value="FFFFFF" />`|
    |<span data-ttu-id="89522-238">Footer background</span><span class="sxs-lookup"><span data-stu-id="89522-238">Footer background</span></span>|<span data-ttu-id="89522-239">Black</span><span class="sxs-lookup"><span data-stu-id="89522-239">Black</span></span>| `<s:color name="FooterBackground" value="000000" />`|

6. <span data-ttu-id="89522-240">To customize .spfont, download a copy of a .spfont file and open it in a text editor.</span><span class="sxs-lookup"><span data-stu-id="89522-240">To customize .spfont, download a copy of a .spfont file and open it in a text editor.</span></span> <span data-ttu-id="89522-241">Notice that the .spfont file is laid out a bit differently than .spcolor, but that both files share a similar structure.</span><span class="sxs-lookup"><span data-stu-id="89522-241">Notice that the .spfont file is laid out a bit differently than .spcolor, but that both files share a similar structure.</span></span> 
    
    <span data-ttu-id="89522-242">**Figure 4. .spfont file**</span><span class="sxs-lookup"><span data-stu-id="89522-242">**Figure 4. .spfont file**</span></span>

    ![Screenshot that shows the contents of the .spfont file](media/893f905a-34d9-4dbd-a012-03797084f9e6.png)

7. <span data-ttu-id="89522-244">Edit each  `<s:fontSlot />` section to customize the font SharePoint applies to the specified font slot on the page.</span><span class="sxs-lookup"><span data-stu-id="89522-244">Edit each  `<s:fontSlot />` section to customize the font SharePoint applies to the specified font slot on the page.</span></span> <span data-ttu-id="89522-245">For example, notice the first entry, `<s:fontSlot name="title">`.</span><span class="sxs-lookup"><span data-stu-id="89522-245">For example, notice the first entry, `<s:fontSlot name="title">`.</span></span> <span data-ttu-id="89522-246">This entry describes which font SharePoint uses to style the title of the page.</span><span class="sxs-lookup"><span data-stu-id="89522-246">This entry describes which font SharePoint uses to style the title of the page.</span></span> <span data-ttu-id="89522-247">This section also specifies which font will be used for different languages.</span><span class="sxs-lookup"><span data-stu-id="89522-247">This section also specifies which font will be used for different languages.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="89522-248">You can upload custom fonts to SharePoint and point each entry to a custom .eot, .woff, .ttf, and .svg file.</span><span class="sxs-lookup"><span data-stu-id="89522-248">You can upload custom fonts to SharePoint and point each entry to a custom .eot, .woff, .ttf, and .svg file.</span></span> 

8. <span data-ttu-id="89522-249">Upload the file to the **Site settings** > **Theme** > **15** folder.</span><span class="sxs-lookup"><span data-stu-id="89522-249">Upload the file to the **Site settings** > **Theme** > **15** folder.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="89522-250">Save the file with a new file name (for example, custom_font.spfont).</span><span class="sxs-lookup"><span data-stu-id="89522-250">Save the file with a new file name (for example, custom_font.spfont).</span></span>

    <span data-ttu-id="89522-251">The following table maps page elements to fonts as they're defined in the .spfont file.</span><span class="sxs-lookup"><span data-stu-id="89522-251">The following table maps page elements to fonts as they're defined in the .spfont file.</span></span>

|<span data-ttu-id="89522-252">**Element**</span><span class="sxs-lookup"><span data-stu-id="89522-252">**Element**</span></span>|<span data-ttu-id="89522-253">**Schriftart**</span><span class="sxs-lookup"><span data-stu-id="89522-253">**Font**</span></span>|<span data-ttu-id="89522-254">**Code**</span><span class="sxs-lookup"><span data-stu-id="89522-254">**Code**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="89522-255">Titel</span><span class="sxs-lookup"><span data-stu-id="89522-255">Title</span></span>|<span data-ttu-id="89522-256">Open Sans</span><span class="sxs-lookup"><span data-stu-id="89522-256">Open Sans</span></span>| `<s:cs typeface="Open Sans" />`|
|<span data-ttu-id="89522-257">Navigation</span><span class="sxs-lookup"><span data-stu-id="89522-257">Navigation</span></span>|<span data-ttu-id="89522-258">Roboto</span><span class="sxs-lookup"><span data-stu-id="89522-258">Roboto</span></span>| `<s:cs typeface="Roboto" />`|
|<span data-ttu-id="89522-259">Headings</span><span class="sxs-lookup"><span data-stu-id="89522-259">Headings</span></span>|<span data-ttu-id="89522-260">Trajan Pro</span><span class="sxs-lookup"><span data-stu-id="89522-260">Trajan Pro</span></span>| `<s:cs typeface="Trajan Pro" />`|
|<span data-ttu-id="89522-261">Body</span><span class="sxs-lookup"><span data-stu-id="89522-261">Body</span></span>|<span data-ttu-id="89522-262">Open Sans</span><span class="sxs-lookup"><span data-stu-id="89522-262">Open Sans</span></span>| `<s:cs typeface="Open Sans" />`|

<span data-ttu-id="89522-263">You might have to ensure that some custom fonts are available to users' browsers.</span><span class="sxs-lookup"><span data-stu-id="89522-263">You might have to ensure that some custom fonts are available to users' browsers.</span></span> <span data-ttu-id="89522-264">For example, if the headings refer to a Trajan Pro font, which is uncommon on most users' computers, add the following font declarations at the top of the <s:fontSlot> declaration.</span><span class="sxs-lookup"><span data-stu-id="89522-264">For example, if the headings refer to a Trajan Pro font, which is uncommon on most users' computers, add the following font declarations at the top of the <s:fontSlot> declaration.</span></span> <span data-ttu-id="89522-265">This will ensure that the correct font is displayed.</span><span class="sxs-lookup"><span data-stu-id="89522-265">This will ensure that the correct font is displayed.</span></span> 

```XML
<s:latin typeface=" Trajan Pro" eotsrc="/SiteAssets/Trajan Pro.eot" woffsrc="/SiteAssets/Trajan Pro.woff" ttfsrc="/SiteAssets/Trajan Pro.ttf" svgsrc="/SiteAssets/Trajan Pro.svg"  />
```

## <a name="add-a-custom-theme-to-sharepoint"></a><span data-ttu-id="89522-266">Add a custom theme to SharePoint</span><span class="sxs-lookup"><span data-stu-id="89522-266">Add a custom theme to SharePoint</span></span>
<span data-ttu-id="89522-267"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="89522-267"></span></span>

<span data-ttu-id="89522-268">After you make your customizations to the master page, .spcolor, and .spfont files, add them to the Composed Looks directory so that SharePoint can access them.</span><span class="sxs-lookup"><span data-stu-id="89522-268">After you make your customizations to the master page, .spcolor, and .spfont files, add them to the Composed Looks directory so that SharePoint can access them.</span></span> 

1. <span data-ttu-id="89522-269">Go to **Site settings**, and under **Web Designer Galleries**, select **Composed Looks**.</span><span class="sxs-lookup"><span data-stu-id="89522-269">Go to **Site settings**, and under **Web Designer Galleries**, select **Composed Looks**.</span></span> 
    
2. <span data-ttu-id="89522-270">Choose the **new item** link at the top left.</span><span class="sxs-lookup"><span data-stu-id="89522-270">Choose the **new item** link at the top left.</span></span> <span data-ttu-id="89522-271">A window opens, as shown in Figure 5.</span><span class="sxs-lookup"><span data-stu-id="89522-271">A window opens, as shown in Figure 5.</span></span>
    
    <span data-ttu-id="89522-272">**Figure 5. Composed looks**</span><span class="sxs-lookup"><span data-stu-id="89522-272">**Figure 5. Composed looks**</span></span>

    ![Screenshot that shows the new composed look page](media/8155ba5d-9492-473d-b153-c3db566cbdec.png)

3. <span data-ttu-id="89522-274">Add a title and a name for your composed look.</span><span class="sxs-lookup"><span data-stu-id="89522-274">Add a title and a name for your composed look.</span></span>
    
4. <span data-ttu-id="89522-275">Complete the remaining field:</span><span class="sxs-lookup"><span data-stu-id="89522-275">Complete the remaining field:</span></span>
    
    - <span data-ttu-id="89522-276">In the **Master Page URL** field, add the URL of the master page you would like the theme to use.</span><span class="sxs-lookup"><span data-stu-id="89522-276">In the **Master Page URL** field, add the URL of the master page you would like the theme to use.</span></span>
    
    - <span data-ttu-id="89522-277">In the **Theme URL** field, add the URL of the .spcolor file.</span><span class="sxs-lookup"><span data-stu-id="89522-277">In the **Theme URL** field, add the URL of the .spcolor file.</span></span>
    
    - <span data-ttu-id="89522-278">In the **Image URL** field, include the URL of an image that you want to use as a background.</span><span class="sxs-lookup"><span data-stu-id="89522-278">In the **Image URL** field, include the URL of an image that you want to use as a background.</span></span> <span data-ttu-id="89522-279">This is not required if your design doesn't call for a background image.</span><span class="sxs-lookup"><span data-stu-id="89522-279">This is not required if your design doesn't call for a background image.</span></span>
    
    - <span data-ttu-id="89522-280">In the **Font Scheme URL** field, include the URL of the .spfont file.</span><span class="sxs-lookup"><span data-stu-id="89522-280">In the **Font Scheme URL** field, include the URL of the .spfont file.</span></span>
    
    - <span data-ttu-id="89522-281">In the **Display Order** field, indicate the order in which the composed look should be displayed.</span><span class="sxs-lookup"><span data-stu-id="89522-281">In the **Display Order** field, indicate the order in which the composed look should be displayed.</span></span>
    
5. <span data-ttu-id="89522-282">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="89522-282">Choose **Save**.</span></span> <span data-ttu-id="89522-283">Your theme entry will now appear in the  **Composed Looks** list.</span><span class="sxs-lookup"><span data-stu-id="89522-283">Your theme entry will now appear in the  **Composed Looks** list.</span></span>
    
<span data-ttu-id="89522-284">After you add your custom theme to as a composed look, users can access the theme and apply it to a site by going to **Site settings** > **Look and Feel** > **Change the look**.</span><span class="sxs-lookup"><span data-stu-id="89522-284">After you add your custom theme to as a composed look, users can access the theme and apply it to a site by going to **Site settings** > **Look and Feel** > **Change the look**.</span></span> <span data-ttu-id="89522-285">Figure 6 shows an example of a **Change the look** section in **Site Settings**.</span><span class="sxs-lookup"><span data-stu-id="89522-285">Figure 6 shows an example of a **Change the look** section in **Site Settings**.</span></span>

<span data-ttu-id="89522-286">**Figure 6. Composed looks available in Change the look**</span><span class="sxs-lookup"><span data-stu-id="89522-286">**Figure 6. Composed looks available in Change the look**</span></span>

![Screenshot that shows the composed looks that are available in Site Settings > Change the look](media/11acb4ea-cff6-483c-890f-8c574e14f29d.png)

## <a name="what-does-the-theming-engine-do-when-a-user-applies-a-composed-look"></a><span data-ttu-id="89522-288">What does the theming engine do when a user applies a composed look?</span><span class="sxs-lookup"><span data-stu-id="89522-288">What does the theming engine do when a user applies a composed look?</span></span>
<span data-ttu-id="89522-289"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="89522-289"></span></span>

<span data-ttu-id="89522-290">When a user applies a composed look, SharePoint copies, transforms, and stores CSS in the content database.</span><span class="sxs-lookup"><span data-stu-id="89522-290">When a user applies a composed look, SharePoint copies, transforms, and stores CSS in the content database.</span></span> <span data-ttu-id="89522-291">It also recolors and stores images in the content database.</span><span class="sxs-lookup"><span data-stu-id="89522-291">It also recolors and stores images in the content database.</span></span> <span data-ttu-id="89522-292">As part of the process of applying a theme to a site, the theming engine pulls color and font values from the specified color palette and font scheme found in the Theme Gallery of the root site.</span><span class="sxs-lookup"><span data-stu-id="89522-292">As part of the process of applying a theme to a site, the theming engine pulls color and font values from the specified color palette and font scheme found in the Theme Gallery of the root site.</span></span> <span data-ttu-id="89522-293">To apply .master page and the master page .preview file (the site layout), the theming engine pulls master pages in the Master Page Gallery that have a corresponding .preview file.</span><span class="sxs-lookup"><span data-stu-id="89522-293">To apply .master page and the master page .preview file (the site layout), the theming engine pulls master pages in the Master Page Gallery that have a corresponding .preview file.</span></span> 

<span data-ttu-id="89522-294">When it applies a composed look, the engine maps the settings specified by specific CSS comments that the theming engine defines.</span><span class="sxs-lookup"><span data-stu-id="89522-294">When it applies a composed look, the engine maps the settings specified by specific CSS comments that the theming engine defines.</span></span> <span data-ttu-id="89522-295">Under the hood, the theming engine saves the background image to Site Assets, scales and compresses JPG and BMP images, and limits the size of GIF and PNG images.</span><span class="sxs-lookup"><span data-stu-id="89522-295">Under the hood, the theming engine saves the background image to Site Assets, scales and compresses JPG and BMP images, and limits the size of GIF and PNG images.</span></span> 

<span data-ttu-id="89522-296">When a composed look is applied to a SharePoint site, SharePoint finds and replaces CSS comment tokens by embedding a value derived from the composed look in the next line in the CSS file after the token.</span><span class="sxs-lookup"><span data-stu-id="89522-296">When a composed look is applied to a SharePoint site, SharePoint finds and replaces CSS comment tokens by embedding a value derived from the composed look in the next line in the CSS file after the token.</span></span> <span data-ttu-id="89522-297">This new value is applied to the SharePoint site.</span><span class="sxs-lookup"><span data-stu-id="89522-297">This new value is applied to the SharePoint site.</span></span>

<span data-ttu-id="89522-298">The following table lists the CSS comment tokens.</span><span class="sxs-lookup"><span data-stu-id="89522-298">The following table lists the CSS comment tokens.</span></span>

|<span data-ttu-id="89522-299">**Token**</span><span class="sxs-lookup"><span data-stu-id="89522-299">**Token**</span></span>|<span data-ttu-id="89522-300">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="89522-300">**Description**</span></span>|<span data-ttu-id="89522-301">**Corresponding ApplyTheme parameter**</span><span class="sxs-lookup"><span data-stu-id="89522-301">**Corresponding ApplyTheme parameter**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="89522-302">/* ReplaceBGImage */</span><span class="sxs-lookup"><span data-stu-id="89522-302">/* ReplaceBGImage */</span></span>|<span data-ttu-id="89522-303">Swaps current background image with the image in the assigned composed look image URL.</span><span class="sxs-lookup"><span data-stu-id="89522-303">Swaps current background image with the image in the assigned composed look image URL.</span></span>|<span data-ttu-id="89522-304">backgroundImageUrl</span><span class="sxs-lookup"><span data-stu-id="89522-304">backgroundImageUrl</span></span>|
|<span data-ttu-id="89522-305">/* ReplaceFont */</span><span class="sxs-lookup"><span data-stu-id="89522-305">/* ReplaceFont */</span></span>|<span data-ttu-id="89522-306">Swaps the current font with one of the fonts found in the font scheme URL of the assigned composed look.</span><span class="sxs-lookup"><span data-stu-id="89522-306">Swaps the current font with one of the fonts found in the font scheme URL of the assigned composed look.</span></span>|<span data-ttu-id="89522-307">fontSchemeUrl</span><span class="sxs-lookup"><span data-stu-id="89522-307">fontSchemeUrl</span></span>|
|<span data-ttu-id="89522-308">/* ReplaceColor */</span><span class="sxs-lookup"><span data-stu-id="89522-308">/* ReplaceColor */</span></span>|<span data-ttu-id="89522-309">Swaps the current color with one of the colors specified in a color slot in the color palette URL of the assigned composed look.</span><span class="sxs-lookup"><span data-stu-id="89522-309">Swaps the current color with one of the colors specified in a color slot in the color palette URL of the assigned composed look.</span></span>|<span data-ttu-id="89522-310">colorPaletteUrl</span><span class="sxs-lookup"><span data-stu-id="89522-310">colorPaletteUrl</span></span>|
|<span data-ttu-id="89522-311">/* RecolorImage */</span><span class="sxs-lookup"><span data-stu-id="89522-311">/* RecolorImage */</span></span>|<span data-ttu-id="89522-312">Recolors images using tinting or filling.</span><span class="sxs-lookup"><span data-stu-id="89522-312">Recolors images using tinting or filling.</span></span> ||

## <a name="see-also"></a><span data-ttu-id="89522-313">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="89522-313">See also</span></span>
<span data-ttu-id="89522-314"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="89522-314"></span></span>

-  [<span data-ttu-id="89522-315">Lösungen für das SharePoint-Websitebranding und die Seitenanpassung</span><span class="sxs-lookup"><span data-stu-id="89522-315">SharePoint site branding and page customization solutions</span></span>](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [<span data-ttu-id="89522-316">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="89522-316">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)
