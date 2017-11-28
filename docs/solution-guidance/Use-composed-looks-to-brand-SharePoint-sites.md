---
title: Verwendung zusammengesetzt sucht nach Marke SharePoint-Websites
ms.date: 11/03/2017
ms.openlocfilehash: ebf4fa0e503cb8c811c6e7ac549d1b89998c1a7d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-composed-looks-to-brand-sharepoint-sites"></a><span data-ttu-id="4955f-102">Verwendung zusammengesetzt sucht nach Marke SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="4955f-102">Use composed looks to brand SharePoint sites</span></span>

<span data-ttu-id="4955f-103">Gelten Sie zusammengesetzten, einschließlich Farben, Schriftarten und eines Hintergrundbilds, um Ihre SharePoint 2013 und SharePoint Online-Websites mithilfe von SharePoint Designmodul.</span><span class="sxs-lookup"><span data-stu-id="4955f-103">Apply composed looks, including colors, fonts, and a background image, to your SharePoint 2013 and SharePoint Online sites by using the SharePoint theming engine.</span></span>

<span data-ttu-id="4955f-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="4955f-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="4955f-105">Sie können Ihre SharePoint-Websites zusammengesetzten zuweisen.</span><span class="sxs-lookup"><span data-stu-id="4955f-105">You can apply composed looks to your SharePoint sites.</span></span> <span data-ttu-id="4955f-106">Zusammengesetzten sind Out-of-Box-Designs, die in SharePoint 2013 und SharePoint Online enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="4955f-106">Composed looks are out-of-the-box themes that are included in SharePoint 2013 and SharePoint Online.</span></span> <span data-ttu-id="4955f-107">Wählen Sie **Websiteeinstellungen**aus, um ein zusammengesetztes Design auf einer SharePoint-Website anzuwenden, > **Aussehen und Verhalten** > **Erscheinungsbild ändern**.</span><span class="sxs-lookup"><span data-stu-id="4955f-107">To apply a composed look to a SharePoint site, select **Site Settings** > **Look and Feel** > **Change the look**.</span></span> <span data-ttu-id="4955f-108">Klicken Sie dann können der Änderung der Assistent aussehen zum Anpassen der Farben, Schriftarten, Gestaltungsvorlage und Hintergrundbild des ein zusammengesetztes Design.</span><span class="sxs-lookup"><span data-stu-id="4955f-108">You can then use the Change the look wizard to customize the colors, fonts, master page, and background image of a composed look.</span></span> <span data-ttu-id="4955f-109">Die Änderung der Assistent aussehen kopiert, überträgt und CSS, in SharePoints-Inhaltsdatenbank gespeichert.</span><span class="sxs-lookup"><span data-stu-id="4955f-109">The Change the look wizard copies, transforms, and stores CSS in SharePoint's content database.</span></span> <span data-ttu-id="4955f-110">Außerdem recolors Bilder und speichert sie in der Inhaltsdatenbank.</span><span class="sxs-lookup"><span data-stu-id="4955f-110">It also recolors images and stores them in the content database.</span></span> 

## <a name="sharepoint-theming-engine"></a><span data-ttu-id="4955f-111">SharePoint-Designmodul</span><span class="sxs-lookup"><span data-stu-id="4955f-111">SharePoint theming engine</span></span>
<span data-ttu-id="4955f-112"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="4955f-112"></span></span>

<span data-ttu-id="4955f-113">SharePoint 2013 Designmodul können Farben, Schriftarten und eines Hintergrundbilds zu einer Website durch Zuordnen dieser Elemente zu einer Gestaltungsvorlage anwenden.</span><span class="sxs-lookup"><span data-stu-id="4955f-113">You can use the SharePoint 2013 theming engine to apply colors, fonts, and a background image to a site by associating those elements with a master page.</span></span>

<span data-ttu-id="4955f-114">In SharePoint 2013 und SharePoint Online ist ein Design ein verbundener XML-Definitionsdateien, einer Bilddatei und eine Masterseite zugeordnet ist, mit denen Sie benutzerdefinierte CSS auf einer Website anwenden.</span><span class="sxs-lookup"><span data-stu-id="4955f-114">In SharePoint 2013 and SharePoint Online, a theme is a connected set of XML definition files, an image file, and an associated master page that you can use to apply custom CSS to a site.</span></span> <span data-ttu-id="4955f-115">Die folgenden XML-Dateien definieren farbplätze und schriftartenplätze, die die Details zu bestimmten Farben und Schriftarten definieren, wie sie auf Formatvorlagen angewendet werden:</span><span class="sxs-lookup"><span data-stu-id="4955f-115">The following XML files define color slots and font slots that define the details of specific colors and fonts as they're applied to styles:</span></span> 

- <span data-ttu-id="4955f-116">.spcolor</span><span class="sxs-lookup"><span data-stu-id="4955f-116">.spcolor</span></span>
    
- <span data-ttu-id="4955f-117">.spfont</span><span class="sxs-lookup"><span data-stu-id="4955f-117">.spfont</span></span>
    
<span data-ttu-id="4955f-118">Sie können Ihre eigenen Dateien Farbe und Schriftart in Ihrer bevorzugten Text-Editor erstellen.</span><span class="sxs-lookup"><span data-stu-id="4955f-118">You can create your own color and font files in your favorite text editor.</span></span>

<span data-ttu-id="4955f-119">In der folgenden Tabelle sind die Elemente des ein zusammengesetztes Design.</span><span class="sxs-lookup"><span data-stu-id="4955f-119">The following table lists the elements of a composed look.</span></span>

|<span data-ttu-id="4955f-120">**Element**</span><span class="sxs-lookup"><span data-stu-id="4955f-120">**Element**</span></span>|<span data-ttu-id="4955f-121">**Datei oder Dateien**</span><span class="sxs-lookup"><span data-stu-id="4955f-121">**File or files**</span></span>|<span data-ttu-id="4955f-122">**Wo sie gespeichert werden**</span><span class="sxs-lookup"><span data-stu-id="4955f-122">**Where it's stored**</span></span>|<span data-ttu-id="4955f-123">**Erforderlich?**</span><span class="sxs-lookup"><span data-stu-id="4955f-123">**Required?**</span></span>|
|:-----|:-----|:-----|:-----|
|<span data-ttu-id="4955f-124">Farbpalette</span><span class="sxs-lookup"><span data-stu-id="4955f-124">Color palette</span></span>|<span data-ttu-id="4955f-125">.spcolor</span><span class="sxs-lookup"><span data-stu-id="4955f-125">.spcolor</span></span>|<span data-ttu-id="4955f-126">Design Gallery\15 Ordner</span><span class="sxs-lookup"><span data-stu-id="4955f-126">Theme Gallery\15 folder</span></span>|<span data-ttu-id="4955f-127">Ja</span><span class="sxs-lookup"><span data-stu-id="4955f-127">Yes</span></span>|
|<span data-ttu-id="4955f-128">Schriftartenschema</span><span class="sxs-lookup"><span data-stu-id="4955f-128">Font scheme</span></span>|<span data-ttu-id="4955f-129">.spfont</span><span class="sxs-lookup"><span data-stu-id="4955f-129">.spfont</span></span>|<span data-ttu-id="4955f-130">Design Gallery\15 Ordner</span><span class="sxs-lookup"><span data-stu-id="4955f-130">Theme Gallery\15 folder</span></span>|<span data-ttu-id="4955f-131">Nein</span><span class="sxs-lookup"><span data-stu-id="4955f-131">No</span></span>|
|<span data-ttu-id="4955f-132">Layout der Website</span><span class="sxs-lookup"><span data-stu-id="4955f-132">Site layout</span></span>|<p><span data-ttu-id="4955f-133">Master</span><span class="sxs-lookup"><span data-stu-id="4955f-133">.master</span></span></p><p><span data-ttu-id="4955f-134">.Preview</span><span class="sxs-lookup"><span data-stu-id="4955f-134">.preview</span></span></p>|<span data-ttu-id="4955f-135">Gestaltungsvorlagenkatalog</span><span class="sxs-lookup"><span data-stu-id="4955f-135">Master Page Gallery</span></span>|<span data-ttu-id="4955f-136">Ja</span><span class="sxs-lookup"><span data-stu-id="4955f-136">Yes</span></span>|
|<span data-ttu-id="4955f-137">Hintergrundbild</span><span class="sxs-lookup"><span data-stu-id="4955f-137">Background image</span></span>|<p><span data-ttu-id="4955f-138">JPG</span><span class="sxs-lookup"><span data-stu-id="4955f-138">.jpg</span></span></p><p><span data-ttu-id="4955f-139">BMP</span><span class="sxs-lookup"><span data-stu-id="4955f-139">.bmp</span></span></p><p><span data-ttu-id="4955f-140">PNG</span><span class="sxs-lookup"><span data-stu-id="4955f-140">.png</span></span></p><p><span data-ttu-id="4955f-141">GIF</span><span class="sxs-lookup"><span data-stu-id="4955f-141">.gif</span></span></p>|<span data-ttu-id="4955f-142">Website-Objekten</span><span class="sxs-lookup"><span data-stu-id="4955f-142">Site assets</span></span>|<span data-ttu-id="4955f-143">Nein</span><span class="sxs-lookup"><span data-stu-id="4955f-143">No</span></span>|
<span data-ttu-id="4955f-144">Benutzer können mithilfe der Änderung des Assistenten aussehen zusammengesetzten auswählen (**Site Settings** > **Aussehen und Verhalten** > **Erscheinungsbild ändern**), der erste Schritte-Benutzeroberfläche oder direkt in im Menü Websiteaktionen.</span><span class="sxs-lookup"><span data-stu-id="4955f-144">Users can select composed looks by using the Change the look wizard (**Site Settings** > **Look and Feel** > **Change the Look**), the Getting Started UI, or directly in the site actions menu.</span></span> <span data-ttu-id="4955f-145">Wenn ein Benutzer ein zusammengesetztes Design auswählt, wendet Designmodul Farben, Schriftarten, Hintergrundbilder, die zugehörigen Master-Seite und der .preview-Datei, die die master-Seite auf der Website zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="4955f-145">When a user selects a composed look, the theming engine applies colors, fonts, background images, the associated .master page, and the .preview file associated with the .master page to the site.</span></span> 

### <a name="color-palettes"></a><span data-ttu-id="4955f-146">Farbpaletten</span><span class="sxs-lookup"><span data-stu-id="4955f-146">Color palettes</span></span>

<span data-ttu-id="4955f-147">Designmodul speichert Farben in Farbpaletten, die von der Datei .spcolor definiert, wie in Abbildung 1 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4955f-147">The theming engine stores colors in color palettes defined by the .spcolor file, as shown in Figure 1.</span></span> <span data-ttu-id="4955f-148">Farbpaletten werden in den Designkatalog der Stammwebsite gespeichert.</span><span class="sxs-lookup"><span data-stu-id="4955f-148">Color palettes are stored in the Theme Gallery of the root site.</span></span> <span data-ttu-id="4955f-149">Eine Farbpalette ist eine Farbe Palette Definitionen und Farbe Steckplätze bestehen bearbeitbaren XML-Datei.</span><span class="sxs-lookup"><span data-stu-id="4955f-149">A color palette is an editable XML file made up of color palette definitions and color slots.</span></span> <span data-ttu-id="4955f-150">Farbe der Palette Metadaten ( `<s:colorPalette>`) definiert die folgenden:</span><span class="sxs-lookup"><span data-stu-id="4955f-150">Color palette metadata ( `<s:colorPalette>`) defines the following:</span></span>

- <span data-ttu-id="4955f-151">Drei Vorschau anzeigen, die definieren, welche Farbe für die Verwendung in einer Vorschau zusammengesetztes Design Steckplätze Slots.</span><span class="sxs-lookup"><span data-stu-id="4955f-151">Three preview slots that define what color slots to use in composed look previews.</span></span>
    
- <span data-ttu-id="4955f-152">Eine **IsInverted** -Eigenschaft, mit der der Palette Designer angeben, ob das Design invertiert ist (dunkler Hintergrund mit heller Text).</span><span class="sxs-lookup"><span data-stu-id="4955f-152">An  **isInverted** property that lets the palette designer specify whether the theme is inverted (dark background with light text).</span></span>
    
- <span data-ttu-id="4955f-153">Der XML-Namespace das Design zugeordnet.</span><span class="sxs-lookup"><span data-stu-id="4955f-153">The XML namespace associated with the theme.</span></span>
    
<span data-ttu-id="4955f-154">Farbplätze definiert zwei Attributesâ€ "Farbe Name und Valueâ€", die einen Namen für die Farbe und RGB-Wert zu definieren.</span><span class="sxs-lookup"><span data-stu-id="4955f-154">Color slots are defined by two attributesâ€”color name and valueâ€”that define a name for the color and its RGB value.</span></span> <span data-ttu-id="4955f-155">Farbplätze haben semantische Namen wie BodyText oder SiteTitle, die einen Bereich einer SharePoint-Seite Hilfe Sie identifizieren, welche Steckplätze entsprechen.</span><span class="sxs-lookup"><span data-stu-id="4955f-155">Color slots have semantic names, such as BodyText or SiteTitle, that help you identify which slots correspond to a region of a SharePoint page.</span></span>

`<s:color name="BodyText" value="444444" />`

<span data-ttu-id="4955f-156">**Abbildung 1. .spcolor-Datei**</span><span class="sxs-lookup"><span data-stu-id="4955f-156">**Figure 1. .spcolor file**</span></span>

![Screenshot einer .spcolor-Datei mit Farbe Name und Value-Attribute](media/16de0716-2e21-471f-b9e5-f461a33b397b.png)

<span data-ttu-id="4955f-158">Zeile 2 der Datei .spcolor definiert den XML-Namespace Steckplätze Vorschau, und gibt an, ob die Farben umgekehrt werden (weisen sie einen hellen Vordergrund auf eine dunkler Hintergrund anstelle einer dunkler Vordergrund auf Hintergrund).</span><span class="sxs-lookup"><span data-stu-id="4955f-158">Line 2 of the .spcolor file defines the XML namespace, preview slots, and whether colors are inverted (they have a light foreground on a dark background instead of a dark foreground on a light background).</span></span> 

<span data-ttu-id="4955f-159">Die .spcolor-Datei enthält 89 farbplätze.</span><span class="sxs-lookup"><span data-stu-id="4955f-159">The .spcolor file contains 89 color slots.</span></span> <span data-ttu-id="4955f-160">Farbplätze können Sie um umfassendere Aspekte der Farbe, einschließlich Durchlässigkeit, mithilfe von Hexadezimalwerte 8 Ziffern zu definieren.</span><span class="sxs-lookup"><span data-stu-id="4955f-160">You can use color slots to define richer aspects of color, including opacity, by using 8-digit hexadecimal values.</span></span> <span data-ttu-id="4955f-161">Beispielsweise grün ist RRGGBB 00FF00 ein 70 Prozent undurchsichtig grüner AARRGGBB 7F00FF00 ist.</span><span class="sxs-lookup"><span data-stu-id="4955f-161">For example, if green is RRGGBB 00FF00, a 70 percent opaque green is AARRGGBB 7F00FF00.</span></span> <span data-ttu-id="4955f-162">Wenn SharePoint einen Steckplatz, den Sie definieren verwendet, werden keine CSS, die darauf verweist Farbe zu ändern.</span><span class="sxs-lookup"><span data-stu-id="4955f-162">If SharePoint uses a slot that you don't define, any CSS that references it won't change color.</span></span> <span data-ttu-id="4955f-163">Wenn ein Steckplatz definiert ist, die nie in CSS verwiesen wird, wird die Farbe nie in der Benutzeroberfläche angezeigt.</span><span class="sxs-lookup"><span data-stu-id="4955f-163">If a slot is defined that is never referenced in CSS, the color is never shown in the UI.</span></span>

<span data-ttu-id="4955f-164">Sie können die .spcolor-Datei in Editor bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="4955f-164">You can edit the .spcolor file in Notepad.</span></span> <span data-ttu-id="4955f-165">Es kann in PowerPoint nicht bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="4955f-165">You cannot edit it in PowerPoint.</span></span>

### <a name="color-palette-tool"></a><span data-ttu-id="4955f-166">Farbe Palette tool</span><span class="sxs-lookup"><span data-stu-id="4955f-166">Color palette tool</span></span>

<span data-ttu-id="4955f-167">Die [Farbe Palette Tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) können zum Visualisieren Designfarben und wie sie auf der Seite zusammenarbeiten.</span><span class="sxs-lookup"><span data-stu-id="4955f-167">You can use the  [color palette tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) to visualize theme colors and how they work together on the page.</span></span> <span data-ttu-id="4955f-168">Verwenden Sie es zum Identifizieren der Farbinformationen können Sie in der farbplätze der Datei .spcolor verwenden und Farben auf einer SharePoint-Website anwenden, ohne alle CSS im Rahmen des Prozesses ändern.</span><span class="sxs-lookup"><span data-stu-id="4955f-168">Use it to identify color information you can use in the color slots of the .spcolor file, and apply colors to a SharePoint site without changing any CSS as part of the process.</span></span>

<span data-ttu-id="4955f-169">Das Tool zeigt die Farben im Hexadezimal-Format, sodass Sie können auf einfache Weise kopieren und fügen den Color-Wert in das entsprechende Element in der Datei .spcolor.</span><span class="sxs-lookup"><span data-stu-id="4955f-169">The tool displays the colors in hexadecimal format, so you can easily copy and paste the color value into the appropriate element in your .spcolor file.</span></span> <span data-ttu-id="4955f-170">Das Tool Farbe Palette können auch ein Hintergrundbild in einem Modell und Umschalten zwischen der Gestaltungsvorlagen seattle.master und oslo.master passen.</span><span class="sxs-lookup"><span data-stu-id="4955f-170">You can also use the color palette tool to fit a background image into a mockup and toggle between the seattle.master and oslo.master master pages.</span></span> 


<span data-ttu-id="4955f-171">**Abbildung 2. Farbe Palette tool**</span><span class="sxs-lookup"><span data-stu-id="4955f-171">**Figure 2. Color palette tool**</span></span>

![Screenshot des Tools Palette Farbe](media/407d8095-20cd-4d9b-be53-493d95b4653c.png)

<span data-ttu-id="4955f-173">Die Datei .spcolor ist die einzige Datei, die für ein neues Design erforderlich ist, jedoch müssen Sie möglicherweise einige benutzerdefinierte Schriftart Deklarationen, je nach die Extrusionstiefe der Entwurfszeit hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="4955f-173">The .spcolor file is the only file that is required for a new theme, but you might need to add some custom font declarations, depending on the depth of your design.</span></span> <span data-ttu-id="4955f-174">Dazu müssen Sie die .spfont-Datei zugreifen.</span><span class="sxs-lookup"><span data-stu-id="4955f-174">To do that, you need to access the .spfont file.</span></span>

### <a name="font-schemes"></a><span data-ttu-id="4955f-175">Schriftartenschemas</span><span class="sxs-lookup"><span data-stu-id="4955f-175">Font schemes</span></span>

<span data-ttu-id="4955f-176">Auf die gleiche Weise, dass Farbpaletten definieren, wie die Farben in zusammengesetzten verwendet werden definieren Schriftartenschemas Schriftarten in der zusammengesetzten.</span><span class="sxs-lookup"><span data-stu-id="4955f-176">In the same way that color palettes define how colors are used in composed looks, font schemes define the fonts in composed looks.</span></span> 

<span data-ttu-id="4955f-177">Schriftartenschemas sind in der .spfont-Datei in den Designkatalog gespeicherten definiert.</span><span class="sxs-lookup"><span data-stu-id="4955f-177">Font schemes are defined in the .spfont file stored in the Theme Gallery.</span></span> <span data-ttu-id="4955f-178">Die .spfont-Datei umfasst die folgenden schriftartenplätze, die den Namen, Schriftart und Skript Werte ein zusammengesetztes Design zu definieren:</span><span class="sxs-lookup"><span data-stu-id="4955f-178">The .spfont file includes the following font slots that define the name, typeface, and script values of a composed look:</span></span>

- <span data-ttu-id="4955f-179">Titel</span><span class="sxs-lookup"><span data-stu-id="4955f-179">Title</span></span>
    
- <span data-ttu-id="4955f-180">Navigation</span><span class="sxs-lookup"><span data-stu-id="4955f-180">Navigation</span></span>
    
- <span data-ttu-id="4955f-181">Kleine-Überschrift</span><span class="sxs-lookup"><span data-stu-id="4955f-181">Small-heading</span></span>
    
- <span data-ttu-id="4955f-182">Überschrift</span><span class="sxs-lookup"><span data-stu-id="4955f-182">Heading</span></span>
    
- <span data-ttu-id="4955f-183">Large-Überschrift</span><span class="sxs-lookup"><span data-stu-id="4955f-183">Large-heading</span></span>
    
- <span data-ttu-id="4955f-184">Body</span><span class="sxs-lookup"><span data-stu-id="4955f-184">Body</span></span>
    
- <span data-ttu-id="4955f-185">Großer Textkörper</span><span class="sxs-lookup"><span data-stu-id="4955f-185">Large-body</span></span>
    
<span data-ttu-id="4955f-186">Schriftarten sind weitere von Skripttyp (z. B. Lateinisch, Arabisch, Kyrillisch) beschränkt.</span><span class="sxs-lookup"><span data-stu-id="4955f-186">Fonts are further scoped by script type (for example, Latin, Arabic, Cyrillic).</span></span> <span data-ttu-id="4955f-187">Unterstützung für Web Schriftarten ist in vier Dateitypen enthalten:</span><span class="sxs-lookup"><span data-stu-id="4955f-187">Web fonts support is included in four file types:</span></span>

- <span data-ttu-id="4955f-188">Eingebettete open Typ EOT)</span><span class="sxs-lookup"><span data-stu-id="4955f-188">Embedded open type (EOT)</span></span>
    
- <span data-ttu-id="4955f-189">Web open Font Format-Datei (WOFF)</span><span class="sxs-lookup"><span data-stu-id="4955f-189">Web open font format file (WOFF)</span></span>
    
- <span data-ttu-id="4955f-190">TrueType-Schriftart (TTF)</span><span class="sxs-lookup"><span data-stu-id="4955f-190">TrueType font (TTF)</span></span>
    
- <span data-ttu-id="4955f-191">Skalierbare Vektorgrafiken (SVG)</span><span class="sxs-lookup"><span data-stu-id="4955f-191">Scalable vector graphics (SVG)</span></span>
    
<span data-ttu-id="4955f-192">Das Schriftartenschema definiert einen großen Vorschaubild und eine kleine Vorschaubild.</span><span class="sxs-lookup"><span data-stu-id="4955f-192">The font scheme defines a large preview image and a small preview image.</span></span> <span data-ttu-id="4955f-193">Sie sind nur für Webschriftarten erforderlich.</span><span class="sxs-lookup"><span data-stu-id="4955f-193">They are required only for web fonts.</span></span>

<span data-ttu-id="4955f-194">**Hinweis**  Sie können die .spfont-Datei in Editor bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="4955f-194">**Note**  You can edit the .spfont file in Notepad.</span></span> <span data-ttu-id="4955f-195">Es kann in PowerPoint nicht bearbeitet werden.</span><span class="sxs-lookup"><span data-stu-id="4955f-195">You cannot edit it in PowerPoint.</span></span>

<span data-ttu-id="4955f-196">Es folgt ein Beispiel einer .spfont-Datei.</span><span class="sxs-lookup"><span data-stu-id="4955f-196">The following is an example of an .spfont file.</span></span>

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

### <a name="site-layout-master-pages-and-corresponding-preview-files"></a><span data-ttu-id="4955f-197">Layout der Website: Masterseiten und entsprechende Vorschaudateien</span><span class="sxs-lookup"><span data-stu-id="4955f-197">Site layout: master pages and corresponding preview files</span></span>

<span data-ttu-id="4955f-198">Designmodul definiert das Layout Website einen durchkomponierten Look basierend auf der Masterseite Master und die entsprechenden .preview-Datei.</span><span class="sxs-lookup"><span data-stu-id="4955f-198">The theming engine defines the site layout of a composed look based on the .master master page and its corresponding .preview file.</span></span> <span data-ttu-id="4955f-199">Wenn die Masterseite für die zusammengesetztes Design definierten seattle.master ist, definiert die Masterseite beispielsweise das Layout der Website.</span><span class="sxs-lookup"><span data-stu-id="4955f-199">For example, if the master page defined for the composed look is seattle.master, that master page defines the layout of the site.</span></span>

<span data-ttu-id="4955f-200">Das Layout der Website entnommen the Master Page Gallery von Masterseiten, die begleitenden .preview Dateien vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="4955f-200">The site layout is pulled from the Master Page Gallery of any master pages that have accompanying .preview files.</span></span> <span data-ttu-id="4955f-201">Eine Datei .preview ist erforderlich für eine Gestaltungsvorlage als Option für die **Änderung des Erscheinungsbilds** Benutzeroberfläche angezeigt werden (**Websiteeinstellungen** > **Aussehen und Verhalten** > **Erscheinungsbild ändern**).</span><span class="sxs-lookup"><span data-stu-id="4955f-201">A .preview file is required for a master page to appear as an option in the **Change the look** UI (**Site Settings** > **Look and Feel** > **Change the look**).</span></span>

<span data-ttu-id="4955f-202">Erstellen Sie eine Gestaltungsvorlage im Dropdown-Menü Layout der Website zur Verfügung zu stellen, eine .preview-Datei, die die master-Seite entspricht.</span><span class="sxs-lookup"><span data-stu-id="4955f-202">To make a master page available from the Site Layout drop-down menu, create a .preview file that corresponds to the .master page.</span></span> <span data-ttu-id="4955f-203">Die Datei .preview Zeigt Miniaturansichten für zusammengesetztes Design und im Vorschaubereich rechts neben der Optionen auf der Seite designbuilder.aspx **Erscheinungsbild ändern** .</span><span class="sxs-lookup"><span data-stu-id="4955f-203">The .preview file displays thumbnail images for the composed look and the preview section to the right of the **Change the look** options on the designbuilder.aspx page.</span></span>

### <a name="background-image"></a><span data-ttu-id="4955f-204">Hintergrundbild</span><span class="sxs-lookup"><span data-stu-id="4955f-204">Background image</span></span>

<span data-ttu-id="4955f-205">Sie können das Hintergrundbild des ein zusammengesetztes Design ändern, indem Sie auf **Ändern**.</span><span class="sxs-lookup"><span data-stu-id="4955f-205">You can change the background image of a composed look by choosing **Change**.</span></span> <span data-ttu-id="4955f-206">Daraufhin wird ein Dialogfeld hochladen, die Sie zum Hochladen einer Bilddatei verwenden können.</span><span class="sxs-lookup"><span data-stu-id="4955f-206">This opens an upload dialog box that you can use to upload an image file.</span></span> <span data-ttu-id="4955f-207">Sie können auch Ihr eigenes Bild auf den Hintergrund Preview ziehen.</span><span class="sxs-lookup"><span data-stu-id="4955f-207">You can also drag your own image onto the background preview.</span></span>

## <a name="create-custom-themes"></a><span data-ttu-id="4955f-208">Erstellen benutzerdefinierter Designs</span><span class="sxs-lookup"><span data-stu-id="4955f-208">Create custom themes</span></span>
<span data-ttu-id="4955f-209"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="4955f-209"></span></span>

<span data-ttu-id="4955f-210">So erstellen Sie ein benutzerdefiniertes Design:</span><span class="sxs-lookup"><span data-stu-id="4955f-210">To create a custom theme:</span></span>

1. <span data-ttu-id="4955f-211">Wechseln Sie auf **websiteeinstellungen**, und klicken Sie unter der Überschrift Web-Designer-Kataloge, wählen Sie **Designs** > **15**.</span><span class="sxs-lookup"><span data-stu-id="4955f-211">Go to **Site settings**, and under the Web Designer Galleries heading, select **Themes** > **15**.</span></span> <span data-ttu-id="4955f-212">Eine Liste der .spcolor und .spfont-Dateien wird angezeigt, wie in Abbildung 3 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4955f-212">A list of .spcolor and .spfont files appears, as shown in Figure 3.</span></span>
    
    <span data-ttu-id="4955f-213">**Abbildung 3. Designkatalog**</span><span class="sxs-lookup"><span data-stu-id="4955f-213">**Figure 3. Theme Gallery**</span></span>

    ![Screenshot von den Designkatalog, der zeigt Fontscheme und Pallette-Dateien](media/76e9b4f3-5838-4cd8-9f2f-33a0c94bfddd.png)

2. <span data-ttu-id="4955f-215">Laden Sie eine Kopie einer der .spcolor-Dateien (beispielsweise Palette001.spcolor), und öffnen Sie es in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="4955f-215">Download a copy of one of the .spcolor files (for example, Palette001.spcolor) and open it in a text editor.</span></span> 
    
3. <span data-ttu-id="4955f-216">Bearbeiten der Datei kopierten .spcolor entsprechend Ihrer Entwurfsrichtlinien.</span><span class="sxs-lookup"><span data-stu-id="4955f-216">Edit the copied .spcolor file to reflect your design guidelines.</span></span> <span data-ttu-id="4955f-217">Angenommen, wenn Sie eine schwarze Schriftart für Textkörper haben, bearbeiten Sie die Datei zur Änderung der Linie `<s:color name="BodyText" value="444444" />` auf `<s:color name="BodyText" value="000000" />`.</span><span class="sxs-lookup"><span data-stu-id="4955f-217">For example, if you have a black font for main body text, edit the file to change the line  `<s:color name="BodyText" value="444444" />` to `<s:color name="BodyText" value="000000" />`.</span></span>
    
4. <span data-ttu-id="4955f-218">Fügen Sie für jedes HTML-Element eine Farbe hinzu.</span><span class="sxs-lookup"><span data-stu-id="4955f-218">For each HTML element, add your color.</span></span> 
    
5. <span data-ttu-id="4955f-219">Wenn Sie fertig sind, laden Sie die .spcolor-Datei mit den **websiteeinstellungen** > **Design** > **15** Ordner.</span><span class="sxs-lookup"><span data-stu-id="4955f-219">When you are done, upload the .spcolor file to the **Site settings** > **Theme** > **15** folder.</span></span>
    
    <span data-ttu-id="4955f-220">**Hinweis**  Speichern Sie die Datei unter einem neuen Namen (beispielsweise custom_palette1.spcolor).</span><span class="sxs-lookup"><span data-stu-id="4955f-220">**Note**  Save the file with a new file name (for example, custom_palette1.spcolor).</span></span>

   <span data-ttu-id="4955f-221">In der folgenden Tabelle ordnet Farben und Seitenelemente ihr Code in der Datei .spcolor.</span><span class="sxs-lookup"><span data-stu-id="4955f-221">The following table maps colors and page elements to their code in the .spcolor file.</span></span> <span data-ttu-id="4955f-222">Es ist eine Teilmenge der Zuordnungen, die in der Datei .spcolor verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="4955f-222">It is a subset of the mappings that are available in the .spcolor file.</span></span>
    

    |<span data-ttu-id="4955f-223">**Element**</span><span class="sxs-lookup"><span data-stu-id="4955f-223">**Element**</span></span>|<span data-ttu-id="4955f-224">**Farbe**</span><span class="sxs-lookup"><span data-stu-id="4955f-224">**Color**</span></span>|<span data-ttu-id="4955f-225">**Code**</span><span class="sxs-lookup"><span data-stu-id="4955f-225">**Code**</span></span>|
    |:-----|:-----|:-----|
    |<span data-ttu-id="4955f-226">Textkörper</span><span class="sxs-lookup"><span data-stu-id="4955f-226">Body text</span></span>|<span data-ttu-id="4955f-227">Schwarz</span><span class="sxs-lookup"><span data-stu-id="4955f-227">Black</span></span>| `<s:color name="BodyText" value="000000" />`|
    |<span data-ttu-id="4955f-228">Globale Navigation Hintergrund</span><span class="sxs-lookup"><span data-stu-id="4955f-228">Global navigation background</span></span>|<span data-ttu-id="4955f-229">Blau</span><span class="sxs-lookup"><span data-stu-id="4955f-229">Blue</span></span>| `<s:color name="HeaderBackground" value="018dff" />`|
    |<span data-ttu-id="4955f-230">Text für die globale navigation</span><span class="sxs-lookup"><span data-stu-id="4955f-230">Global navigation text</span></span>|<span data-ttu-id="4955f-231">Whitepaper</span><span class="sxs-lookup"><span data-stu-id="4955f-231">White</span></span>| `<s:color name="HeaderNavigationText" value="ffffff" />`|
    |<span data-ttu-id="4955f-232">Aktuelle Navigation Hintergrund</span><span class="sxs-lookup"><span data-stu-id="4955f-232">Current navigation background</span></span>|<span data-ttu-id="4955f-233">Rot</span><span class="sxs-lookup"><span data-stu-id="4955f-233">Red</span></span>| `<s:color name="NavigationHoverBackground" value="e51400" />`|
    |<span data-ttu-id="4955f-234">Text für die aktuelle navigation</span><span class="sxs-lookup"><span data-stu-id="4955f-234">Current navigation text</span></span>|<span data-ttu-id="4955f-235">Whitepaper</span><span class="sxs-lookup"><span data-stu-id="4955f-235">White</span></span>| `<s:color name="Navigation" value="ffffff" />`|
    |<span data-ttu-id="4955f-236">Titel</span><span class="sxs-lookup"><span data-stu-id="4955f-236">Title</span></span>|<span data-ttu-id="4955f-237">Whitepaper</span><span class="sxs-lookup"><span data-stu-id="4955f-237">White</span></span>| `<s:color name="SiteTitle" value="FFFFFF" />`|
    |<span data-ttu-id="4955f-238">Fußzeile Hintergrund</span><span class="sxs-lookup"><span data-stu-id="4955f-238">Footer background</span></span>|<span data-ttu-id="4955f-239">Schwarz</span><span class="sxs-lookup"><span data-stu-id="4955f-239">Black</span></span>| `<s:color name="FooterBackground" value="000000" />`|

6. <span data-ttu-id="4955f-240">Informationen zum Anpassen von .spfont Herunterladen einer Kopie einer .spfont-Datei, und öffnen Sie es in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="4955f-240">To customize .spfont, download a copy of a .spfont file and open it in a text editor.</span></span> <span data-ttu-id="4955f-241">Beachten Sie, dass die .spfont-Datei ein wenig anders als .spcolor angeordnet ist, aber beide Dateien eine ähnliche Struktur freigeben.</span><span class="sxs-lookup"><span data-stu-id="4955f-241">Notice that the .spfont file is laid out a bit differently than .spcolor, but that both files share a similar structure.</span></span> 
    
    <span data-ttu-id="4955f-242">**Abbildung 4. .spfont-Datei**</span><span class="sxs-lookup"><span data-stu-id="4955f-242">**Figure 4. .spfont file**</span></span>

    ![Screenshot, der den Inhalt der .spfont-Datei anzeigt](media/893f905a-34d9-4dbd-a012-03797084f9e6.png)

7. <span data-ttu-id="4955f-244">Bearbeiten Sie jede `<s:fontSlot />` Abschnitt zum Anpassen der Schriftart SharePoint gilt für die angegebene Schriftart Steckplatz auf der Seite.</span><span class="sxs-lookup"><span data-stu-id="4955f-244">Edit each  `<s:fontSlot />` section to customize the font SharePoint applies to the specified font slot on the page.</span></span> <span data-ttu-id="4955f-245">Beachten Sie beispielsweise den ersten Eintrag, `<s:fontSlot name="title">`.</span><span class="sxs-lookup"><span data-stu-id="4955f-245">For example, notice the first entry, `<s:fontSlot name="title">`.</span></span> <span data-ttu-id="4955f-246">Dieser Eintrag wird beschrieben, welche Schriftart SharePoint verwendet, um den Titel der Seite zu formatieren.</span><span class="sxs-lookup"><span data-stu-id="4955f-246">This entry describes which font SharePoint uses to style the title of the page.</span></span> <span data-ttu-id="4955f-247">In diesem Abschnitt gibt auch an, welche Schriftart für verschiedene Sprachen verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="4955f-247">This section also specifies which font will be used for different languages.</span></span>
    
    <span data-ttu-id="4955f-248">**Hinweis**  Sie können hochladen benutzerdefinierte Schriftarten in SharePoint und zeigen Sie jeden Eintrag auf eine benutzerdefinierte .eot, .woff, ttf und SVG-Datei.</span><span class="sxs-lookup"><span data-stu-id="4955f-248">**Note**  You can upload custom fonts to SharePoint and point each entry to a custom .eot, .woff, .ttf, and .svg file.</span></span> 

8. <span data-ttu-id="4955f-249">Laden Sie die Datei mit den **websiteeinstellungen** > **Design** > **15** Ordner.</span><span class="sxs-lookup"><span data-stu-id="4955f-249">Upload the file to the **Site settings** > **Theme** > **15** folder.</span></span>
    
    <span data-ttu-id="4955f-250">**Hinweis**  Speichern Sie die Datei unter einem neuen Namen (beispielsweise custom_font.spfont).</span><span class="sxs-lookup"><span data-stu-id="4955f-250">**Note**  Save the file with a new file name (for example, custom_font.spfont).</span></span>

    <span data-ttu-id="4955f-251">In der folgenden Tabelle ordnet Schriftarten Seitenelemente wie sie in der .spfont-Datei definiert sind.</span><span class="sxs-lookup"><span data-stu-id="4955f-251">The following table maps page elements to fonts as they're defined in the .spfont file.</span></span>

|<span data-ttu-id="4955f-252">**Element**</span><span class="sxs-lookup"><span data-stu-id="4955f-252">**Element**</span></span>|<span data-ttu-id="4955f-253">**Schriftart**</span><span class="sxs-lookup"><span data-stu-id="4955f-253">**Font**</span></span>|<span data-ttu-id="4955f-254">**Code**</span><span class="sxs-lookup"><span data-stu-id="4955f-254">**Code**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="4955f-255">Titel</span><span class="sxs-lookup"><span data-stu-id="4955f-255">Title</span></span>|<span data-ttu-id="4955f-256">Sans öffnen</span><span class="sxs-lookup"><span data-stu-id="4955f-256">Open Sans</span></span>| `<s:cs typeface="Open Sans" />`|
|<span data-ttu-id="4955f-257">Navigation</span><span class="sxs-lookup"><span data-stu-id="4955f-257">Navigation</span></span>|<span data-ttu-id="4955f-258">Roboto</span><span class="sxs-lookup"><span data-stu-id="4955f-258">Roboto</span></span>| `<s:cs typeface="Roboto" />`|
|<span data-ttu-id="4955f-259">Überschriften</span><span class="sxs-lookup"><span data-stu-id="4955f-259">Headings</span></span>|<span data-ttu-id="4955f-260">Trajan Pro</span><span class="sxs-lookup"><span data-stu-id="4955f-260">Trajan Pro</span></span>| `<s:cs typeface="Trajan Pro" />`|
|<span data-ttu-id="4955f-261">Body</span><span class="sxs-lookup"><span data-stu-id="4955f-261">Body</span></span>|<span data-ttu-id="4955f-262">Sans öffnen</span><span class="sxs-lookup"><span data-stu-id="4955f-262">Open Sans</span></span>| `<s:cs typeface="Open Sans" />`|

<span data-ttu-id="4955f-263">Möglicherweise müssen Sie sicherstellen, dass einige benutzerdefinierten Schriftarten Browser Benutzer zur Verfügung stehen.</span><span class="sxs-lookup"><span data-stu-id="4955f-263">You might have to ensure that some custom fonts are available to users' browsers.</span></span> <span data-ttu-id="4955f-264">Bezieht sich die Überschriften auf eine Trajan Pro Schriftart, die auf die meisten Benutzercomputern ungewöhnlich ist, fügen Sie die folgenden Deklarationen von Schriftart am oberen Rand der Deklaration < S:fontSlot > fest.</span><span class="sxs-lookup"><span data-stu-id="4955f-264">For example, if the headings refer to a Trajan Pro font, which is uncommon on most users' computers, add the following font declarations at the top of the <s:fontSlot> declaration.</span></span> <span data-ttu-id="4955f-265">Dadurch wird sichergestellt, dass die richtige Schriftart angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="4955f-265">This will ensure that the correct font is displayed.</span></span> 

```XML
<s:latin typeface=" Trajan Pro" eotsrc="/SiteAssets/Trajan Pro.eot" woffsrc="/SiteAssets/Trajan Pro.woff" ttfsrc="/SiteAssets/Trajan Pro.ttf" svgsrc="/SiteAssets/Trajan Pro.svg"  />
```

## <a name="add-a-custom-theme-to-sharepoint"></a><span data-ttu-id="4955f-266">Hinzufügen eines benutzerdefinierten Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="4955f-266">Add a custom theme to SharePoint</span></span>
<span data-ttu-id="4955f-267"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="4955f-267"></span></span>

<span data-ttu-id="4955f-268">Nachdem Sie Ihre Anpassungen an der Gestaltungsvorlage, .spcolor und .spfont-Dateien vornehmen, fügen sie in das Verzeichnis zusammengesetzten hinzu, damit SharePoint, darauf zugreifen kann.</span><span class="sxs-lookup"><span data-stu-id="4955f-268">After you make your customizations to the master page, .spcolor, and .spfont files, add them to the Composed Looks directory so that SharePoint can access them.</span></span> 

1. <span data-ttu-id="4955f-269">Wechseln Sie auf **websiteeinstellungen**, und klicken Sie unter **Web-Designer-Kataloge**, und wählen Sie **Zusammengesetzten**.</span><span class="sxs-lookup"><span data-stu-id="4955f-269">Go to **Site settings**, and under **Web Designer Galleries**, select **Composed Looks**.</span></span> 
    
2. <span data-ttu-id="4955f-270">Wählen Sie den Link **Neues Element** oben links aus.</span><span class="sxs-lookup"><span data-stu-id="4955f-270">Choose the **new item** link at the top left.</span></span> <span data-ttu-id="4955f-271">Ein Fenster geöffnet wird, wie in Abbildung 5 dargestellt.</span><span class="sxs-lookup"><span data-stu-id="4955f-271">A window opens, as shown in Figure 5.</span></span>
    
    <span data-ttu-id="4955f-272">**Abbildung 5. Zusammengesetzten**</span><span class="sxs-lookup"><span data-stu-id="4955f-272">**Figure 5. Composed looks**</span></span>

    ![Screenshot, der auf der Seite neue zusammengesetztes Design wird](media/8155ba5d-9492-473d-b153-c3db566cbdec.png)

3. <span data-ttu-id="4955f-274">Fügen Sie einen Titel und einen Namen für Ihre zusammengesetztes Design.</span><span class="sxs-lookup"><span data-stu-id="4955f-274">Add a title and a name for your composed look.</span></span>
    
4. <span data-ttu-id="4955f-275">Führen Sie das verbleibende dar:</span><span class="sxs-lookup"><span data-stu-id="4955f-275">Complete the remaining field:</span></span>
    
    - <span data-ttu-id="4955f-276">Fügen Sie im Feld **Master-Seiten-URL** die URL der Masterseite, die Sie Designs verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="4955f-276">In the **Master Page URL** field, add the URL of the master page you would like the theme to use.</span></span>
    
    - <span data-ttu-id="4955f-277">Fügen Sie im Feld **Design-URL** die URL der Datei .spcolor hinzu.</span><span class="sxs-lookup"><span data-stu-id="4955f-277">In the **Theme URL** field, add the URL of the .spcolor file.</span></span>
    
    - <span data-ttu-id="4955f-278">Schließen Sie im Feld **Bild-URL** die URL eines Bilds, das Sie als Hintergrund verwenden möchten.</span><span class="sxs-lookup"><span data-stu-id="4955f-278">In the **Image URL** field, include the URL of an image that you want to use as a background.</span></span> <span data-ttu-id="4955f-279">Dies ist nicht erforderlich, wenn Ihre Umgebung für ein Hintergrundbild Aufrufen nicht.</span><span class="sxs-lookup"><span data-stu-id="4955f-279">This is not required if your design doesn't call for a background image.</span></span>
    
    - <span data-ttu-id="4955f-280">Schließen Sie in das Feld **Schriftart Schema URL** die URL der .spfont-Datei.</span><span class="sxs-lookup"><span data-stu-id="4955f-280">In the **Font Scheme URL** field, include the URL of the .spfont file.</span></span>
    
    - <span data-ttu-id="4955f-281">Geben Sie im Feld **Anzeigereihenfolge** an, die Reihenfolge, in der zusammengesetzte Design angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="4955f-281">In the **Display Order** field, indicate the order in which the composed look should be displayed.</span></span>
    
5. <span data-ttu-id="4955f-282">Wählen Sie **Speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="4955f-282">Choose **Save**.</span></span> <span data-ttu-id="4955f-283">Ihre Eingabe Design wird nun in der Liste **Durchkomponierte** angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="4955f-283">Your theme entry will now appear in the  **Composed Looks** list.</span></span>
    
<span data-ttu-id="4955f-284">Nach dem Hinzufügen Ihrer benutzerdefinierten Designs aus, um als ein zusammengesetztes Design Benutzer das Design zugreifen und es zu einer Website anwenden, indem Sie auf **websiteeinstellungen** > **Aussehen und Verhalten** > **Erscheinungsbild ändern**.</span><span class="sxs-lookup"><span data-stu-id="4955f-284">After you add your custom theme to as a composed look, users can access the theme and apply it to a site by going to **Site settings** > **Look and Feel** > **Change the look**.</span></span> <span data-ttu-id="4955f-285">Abbildung 6 zeigt ein Beispiel eines Abschnitts **Erscheinungsbild ändern** , in den **Websiteeinstellungen**.</span><span class="sxs-lookup"><span data-stu-id="4955f-285">Figure 6 shows an example of a **Change the look** section in **Site Settings**.</span></span>

<span data-ttu-id="4955f-286">**Abbildung 6. Zusammengesetzten in Erscheinungsbild ändern verfügbar**</span><span class="sxs-lookup"><span data-stu-id="4955f-286">**Figure 6. Composed looks available in Change the look**</span></span>

![Screenshot, der anzeigt, die zusammengesetzten sucht, stehen in den Websiteeinstellungen > Ändern der Darstellung](media/11acb4ea-cff6-483c-890f-8c574e14f29d.png)

## <a name="what-does-the-theming-engine-do-when-a-user-applies-a-composed-look"></a><span data-ttu-id="4955f-288">Was geschieht Designmodul? Wenn ein Benutzer ein zusammengesetztes Design angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="4955f-288">What does the theming engine do when a user applies a composed look?</span></span>
<span data-ttu-id="4955f-289"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="4955f-289"></span></span>

<span data-ttu-id="4955f-290">Wenn ein Benutzer ein zusammengesetztes Design angewendet wird, wird SharePoint kopiert, überträgt und speichert in der Inhaltsdatenbank CSS.</span><span class="sxs-lookup"><span data-stu-id="4955f-290">When a user applies a composed look, SharePoint copies, transforms, and stores CSS in the content database.</span></span> <span data-ttu-id="4955f-291">Außerdem recolors und speichert Bilder in der Inhaltsdatenbank.</span><span class="sxs-lookup"><span data-stu-id="4955f-291">It also recolors and stores images in the content database.</span></span> <span data-ttu-id="4955f-292">Im Rahmen des Prozesses zum Anwenden eines Designs auf eine Website zieht Designmodul Farbe und Schriftart Werte aus der angegebenen Farbe Farbpalette und ein Schriftartenschema in den Designkatalog der Stammwebsite gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="4955f-292">As part of the process of applying a theme to a site, the theming engine pulls color and font values from the specified color palette and font scheme found in the Theme Gallery of the root site.</span></span> <span data-ttu-id="4955f-293">Zum Anwenden von Master-Seite und die .preview Gestaltungsvorlagendatei (das Layout der Website) zieht Designmodul Gestaltungsvorlagen in the Master Page Gallery, die eine entsprechende Datei .preview aufweisen.</span><span class="sxs-lookup"><span data-stu-id="4955f-293">To apply .master page and the master page .preview file (the site layout), the theming engine pulls master pages in the Master Page Gallery that have a corresponding .preview file.</span></span> 

<span data-ttu-id="4955f-294">Wenn sie ein zusammengesetztes Design angewendet wird, ordnet das Modul die Einstellungen, die durch bestimmte CSS-Kommentare, die Designmodul definiert angegeben.</span><span class="sxs-lookup"><span data-stu-id="4955f-294">When it applies a composed look, the engine maps the settings specified by specific CSS comments that the theming engine defines.</span></span> <span data-ttu-id="4955f-295">Designmodul im Detail speichert das Hintergrundbild auf Website-Objekten, skalierbar und JPG und BMP Bilder komprimiert und beschränkt die Größe von GIF und PNG-Bilder.</span><span class="sxs-lookup"><span data-stu-id="4955f-295">Under the hood, the theming engine saves the background image to Site Assets, scales and compresses JPG and BMP images, and limits the size of GIF and PNG images.</span></span> 

<span data-ttu-id="4955f-296">Wenn ein zusammengesetztes Design auf einer SharePoint-Website angewendet wird, SharePoint sucht und CSS-Kommentartoken durch Einbetten eines Werts, der die zusammengesetztes Design in die nächste Zeile in der CSS-Datei nach dem Token abgeleiteten ersetzt.</span><span class="sxs-lookup"><span data-stu-id="4955f-296">When a composed look is applied to a SharePoint site, SharePoint finds and replaces CSS comment tokens by embedding a value derived from the composed look in the next line in the CSS file after the token.</span></span> <span data-ttu-id="4955f-297">In diesem neue Wert wird auf der SharePoint-Website angewendet.</span><span class="sxs-lookup"><span data-stu-id="4955f-297">This new value is applied to the SharePoint site.</span></span>

<span data-ttu-id="4955f-298">Die folgende Tabelle enthält die CSS-Kommentar-Token.</span><span class="sxs-lookup"><span data-stu-id="4955f-298">The following table lists the CSS comment tokens.</span></span>

|<span data-ttu-id="4955f-299">**Token**</span><span class="sxs-lookup"><span data-stu-id="4955f-299">**Token**</span></span>|<span data-ttu-id="4955f-300">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="4955f-300">**Description**</span></span>|<span data-ttu-id="4955f-301">**Entsprechende ApplyTheme-parameter**</span><span class="sxs-lookup"><span data-stu-id="4955f-301">**Corresponding ApplyTheme parameter**</span></span>|
|:-----|:-----|:-----|
|<span data-ttu-id="4955f-302">/ * ReplaceBGImage * /</span><span class="sxs-lookup"><span data-stu-id="4955f-302">/* ReplaceBGImage */</span></span>|<span data-ttu-id="4955f-303">Aktuelle Hintergrundbild mit dem Bild in der zugewiesenen vertauscht zusammengesetzt aussehen Bild-URL.</span><span class="sxs-lookup"><span data-stu-id="4955f-303">Swaps current background image with the image in the assigned composed look image URL.</span></span>|<span data-ttu-id="4955f-304">backgroundImageUrl</span><span class="sxs-lookup"><span data-stu-id="4955f-304">backgroundImageUrl</span></span>|
|<span data-ttu-id="4955f-305">/ * ReplaceFont * /</span><span class="sxs-lookup"><span data-stu-id="4955f-305">/* ReplaceFont */</span></span>|<span data-ttu-id="4955f-306">Wechselt von der aktuellen Schriftart mit einem der Schriftarten, die in der Schriftart Schema URL von der zugewiesenen zusammengesetztes Design gefunden.</span><span class="sxs-lookup"><span data-stu-id="4955f-306">Swaps the current font with one of the fonts found in the font scheme URL of the assigned composed look.</span></span>|<span data-ttu-id="4955f-307">fontSchemeUrl</span><span class="sxs-lookup"><span data-stu-id="4955f-307">fontSchemeUrl</span></span>|
|<span data-ttu-id="4955f-308">/ * ReplaceColor * /</span><span class="sxs-lookup"><span data-stu-id="4955f-308">/* ReplaceColor */</span></span>|<span data-ttu-id="4955f-309">Vertauscht die aktuelle Farbe mit einem der in einer farbplatzes in der Farbe Palette URL von der zugewiesenen zusammengesetztes Design angegebenen Farben.</span><span class="sxs-lookup"><span data-stu-id="4955f-309">Swaps the current color with one of the colors specified in a color slot in the color palette URL of the assigned composed look.</span></span>|<span data-ttu-id="4955f-310">colorPaletteUrl</span><span class="sxs-lookup"><span data-stu-id="4955f-310">colorPaletteUrl</span></span>|
|<span data-ttu-id="4955f-311">/ * RecolorImage * /</span><span class="sxs-lookup"><span data-stu-id="4955f-311">/* RecolorImage */</span></span>|<span data-ttu-id="4955f-312">Recolors Bilder mit Farbton anpassen oder ausfüllen.</span><span class="sxs-lookup"><span data-stu-id="4955f-312">Recolors images using tinting or filling.</span></span> ||

## <a name="additional-resources"></a><span data-ttu-id="4955f-313">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="4955f-313">Additional resources</span></span>
<span data-ttu-id="4955f-314"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="4955f-314"></span></span>

-  [<span data-ttu-id="4955f-315">Lösungen für das SharePoint-Websitebranding und die Seitenanpassung</span><span class="sxs-lookup"><span data-stu-id="4955f-315">SharePoint site branding and page customization solutions</span></span>](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [<span data-ttu-id="4955f-316">Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website</span><span class="sxs-lookup"><span data-stu-id="4955f-316">Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online</span></span>](Branding-and-site-provisioning-solutions-for-SharePoint.md)
