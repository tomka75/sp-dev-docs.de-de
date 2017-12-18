---
title: Gestalten von flexiblen benutzerdefinierten CSS-Dateien in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b8c82c77-c836-47f9-a11e-6c9c656d436b
ms.openlocfilehash: 6a2febe12c0420a75024937b3127504ca00592f6
ms.sourcegitcommit: f6ea922341c38e700d0697961f8df9a454a03cba
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2017
---
# <a name="make-custom-css-files-themable-in-sharepoint"></a><span data-ttu-id="e837c-102">Gestalten von flexiblen benutzerdefinierten CSS-Dateien in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e837c-102">How to: Make custom CSS files themable in SharePoint</span></span>

<span data-ttu-id="e837c-103">Erfahren Sie mehr über das Hinzufügen von Kommentarstil-Markups zu einer CSS-Datei, sodass sie im SharePoint-Designmodul verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="e837c-103">Learn how to add comment-style markup to a CSS file so that it can be used in the SharePoint theming engine.</span></span>

## <a name="introduction-to-annotations"></a><span data-ttu-id="e837c-104">Einführung in Anmerkungen</span><span class="sxs-lookup"><span data-stu-id="e837c-104">Introduction to annotations</span></span>
<span data-ttu-id="e837c-105"><a name="Intro"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-105"><a name="Intro"> </a></span></span>

<span data-ttu-id="e837c-p101">Anmerkungen sind spezielle Kommentarstil-Markups, die dem SharePoint-Designmodul mitteilen, wie die Eigenschaften in einer CSS-Datei gestaltet werden sollen. Wenn ein Design auf eine Website angewendet wird, ersetzt das Designmodul die CSS-Eigenschaftswerte durch die entsprechenden Designwerte. In SharePoint können Sie Anmerkungen verwenden, um die Farbe, die Schriftart oder das Hintergrundbild zu ändern. Sie können ein Bild auch neu einfärben. Bei Verwendung benutzerdefinierter CSS-Dateien müssen Sie diese Anmerkungen zu den CSS-Dateien hinzufügen, wenn Sie sie mit dem SharePoint-Designmodul verwenden möchten. Wenn Sie ein Design auf eine Website anwenden, die benutzerdefinierte CSS-Dateien verwendet, und Sie keine Anmerkungen hinzugefügt haben, bleiben die CSS-Eigenschaften unverändert. Das kann zu einem unstimmigen Design der Website führen.</span><span class="sxs-lookup"><span data-stu-id="e837c-p101">Annotations are special comment-style markup that tell the SharePoint theming engine how to theme properties in a CSS file. When a theme is applied to a site, the theming engine replaces the CSS property values with the appropriate theme values. In SharePoint, you can use annotations to change the color, font, or background image. You can also recolor an image. If you are using custom CSS files, you must add these annotations to the CSS files if you want to use them with the SharePoint theming engine. If you apply a theme to a site that uses custom CSS files, and you haven't added annotations, the CSS properties remain unchanged. This can result in a site that has a mismatched design.</span></span>
  
    
    
<span data-ttu-id="e837c-113">In diesem Artikel werden die verfügbaren Anmerkungen und die Vorgehensweise zum Registrieren von CSS-Dateien beschrieben.</span><span class="sxs-lookup"><span data-stu-id="e837c-113">This article describes the available annotations and how to register CSS files.</span></span>
  
    
    
<span data-ttu-id="e837c-114">Weitere Informationen zu benutzerdefinierten Designs finden Sie unter  [Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) und [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e837c-114">For more information about custom themes, see  [How to: Deploy a custom theme in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) and [How to: Create a master page preview file in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).</span></span>
  
    
    

## <a name="add-annotations-to-custom-css-files"></a><span data-ttu-id="e837c-115">Hinzufügen von Anmerkungen zu benutzerdefinierten CSS-Dateien</span><span class="sxs-lookup"><span data-stu-id="e837c-115">Add annotations to custom CSS files</span></span>
<span data-ttu-id="e837c-116"><a name="annotations"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-116"><a name="annotations"> </a></span></span>

<span data-ttu-id="e837c-p102">Anmerkungen teilen dem SharePoint-Designmodul mit, wie die Eigenschaften in einer CSS-Datei gestaltet werden sollen. In diesem Abschnitt werden die verfügbaren Anmerkungen und ihre Verwendungsweise erläutert.</span><span class="sxs-lookup"><span data-stu-id="e837c-p102">Annotations tell the SharePoint theming engine how to theme properties in a CSS file. This section describes the available annotations and how they can be used.</span></span>
  
    
    

### <a name="replacecolor-annotation"></a><span data-ttu-id="e837c-119">ReplaceColor-Anmerkung</span><span class="sxs-lookup"><span data-stu-id="e837c-119">ReplaceColor annotation</span></span>
<span data-ttu-id="e837c-120"><a name="replaceColor"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-120"><a name="replaceColor"> </a></span></span>

<span data-ttu-id="e837c-p103">Die **ReplaceColor** -Anmerkung ersetzt den Farbwert durch die angegebene Designfarbe. Sie kann mit CSS-Eigenschaften verwendet werden, die einen Farbwert definieren, wie z. B. **color**, **background-color**, **border** usw.</span><span class="sxs-lookup"><span data-stu-id="e837c-p103">The **ReplaceColor** annotation replaces the color value with the specified theme color. It can be used with CSS properties that define a color value, such as **color**, **background-color**, **border**, and so on.</span></span>
  
    
    
<span data-ttu-id="e837c-123">Im Folgenden ist das Format für die **ReplaceColor**-Anmerkung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="e837c-123">The following shows the format for the **ReplaceColor** annotation.</span></span>
  
    
    



```

/* [ReplaceColor(themeColor:"ColorSlot"[, themeShade:"ShadeValue"][, themeTint:"TintValue"][, opacity:"OpacityValue"])] */

```

<span data-ttu-id="e837c-p104">Ersetzen Sie  _ColorSlot_ durch den Anmerkungsnamen des zu verwendenden Farbplatzes. Eine Liste der verfügbaren Farbplätze finden Sie im Abschnitt [Zuordnen von Farbplätzen](color-palettes-and-fonts-in-sharepoint.md#colorSlots) in [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e837c-p104">Replace  _ColorSlot_ with the annotation name of the color slot to use. To see a list of available color slots, see the [Color slot mapping](color-palettes-and-fonts-in-sharepoint.md#colorSlots) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="e837c-p105">Verwenden Sie den optionalen **themeShade** -Parameter, wenn Sie die Designfarbe abdunkeln möchten. Ersetzen Sie _ShadeValue_ durch einen numerischen Wert von 0,0 (keine Änderung) bis 1,0 (dunkelste Schattierung).</span><span class="sxs-lookup"><span data-stu-id="e837c-p105">Use the optional **themeShade** parameter if you want to darken the theme color. Replace _ShadeValue_ with a numeric value from 0.0 (no change) to 1.0 (darkest).</span></span>
  
    
    
<span data-ttu-id="e837c-p106">Verwenden Sie den optionalen **themeTint** -Parameter, wenn Sie die Designfarbe aufhellen möchten. Ersetzen Sie _TintValue_ durch einen numerischen Wert von 0,0 (keine Änderung) bis 1,0 (hellste Schattierung).</span><span class="sxs-lookup"><span data-stu-id="e837c-p106">Use the optional **themeTint** parameter if you want to lighten the theme color. Replace _TintValue_ with a numeric value from 0.0 (no change) to 1.0 (lightest).</span></span>
  
    
    
<span data-ttu-id="e837c-p107">Verwenden Sie den optionalen **opacity** -Parameter, wenn Sie die Deckkraft der Designfarbe angeben möchten. Ersetzen Sie _OpacityValue_ durch einen numerischen Wert, der die Deckkrafteinstellung angibt. Der Bereich der Deckkrafteinstellung liegt zwischen 0,0 (vollständig transparent) und 1,0 (vollständig deckend).</span><span class="sxs-lookup"><span data-stu-id="e837c-p107">Use the optional **opacity** parameter if you want to specify the opacity of the theme color. Replace _OpacityValue_ with a numeric value that specifies the opacity setting. The opacity setting ranges from 0.0 (fully transparent) to 1.0 (fully opaque).</span></span>
  
    
    
<span data-ttu-id="e837c-133">Im Folgenden finden Sie Beispiele für die Verwendung der **ReplaceColor** -Anmerkung in einer CSS-Datei.</span><span class="sxs-lookup"><span data-stu-id="e837c-133">The following shows examples of the **ReplaceColor** annotation being used in a CSS file.</span></span>
  
    
    

-  `/* [ReplaceColor(themeColor:"BodyText")] */ color:#444;`
    
  
-  `/* [ReplaceColor(themeColor:"BackgroundOverlay",opacity:"0.5")] */ background-color:#fff;`
    
  
-  `/* [ReplaceColor(themeColor:"EmphasisBackground",themeTint:"0.05")] */ background-color:#f2faff;`
    
  

### <a name="replacefont-annotation"></a><span data-ttu-id="e837c-134">ReplaceFont-Anmerkung</span><span class="sxs-lookup"><span data-stu-id="e837c-134">ReplaceFont annotation</span></span>
<span data-ttu-id="e837c-135"><a name="replaceFont"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-135"><a name="replaceFont"> </a></span></span>

<span data-ttu-id="e837c-p108">Die **ReplaceFont** -Anmerkung fügt die angegebene Designschriftfarbe zur Liste der verfügbaren Schriftarten hinzu. Sie kann mit den CSS-Eigenschaften **font** und **font-family** verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e837c-p108">The **ReplaceFont** annotation adds the specified theme font to the list of available fonts. It can be used with the **font** and **font-family** CSS properties.</span></span>
  
    
    
<span data-ttu-id="e837c-138">Im Folgenden ist das Format für die **ReplaceFont** -Anmerkung dargestellt.</span><span class="sxs-lookup"><span data-stu-id="e837c-138">The following shows the format for the **ReplaceFont** annotation.</span></span>
  
    
    



```

/* [ReplaceFont(themeFont:"FontSlot")] */
```

<span data-ttu-id="e837c-p109">Ersetzen Sie  _FontSlot_ durch den Namen des zu verwendenden Schriftartenplatzes. Eine Liste der verfügbaren Schriftartenplätze finden Sie im Abschnitt [Schriftartenplätze](color-palettes-and-fonts-in-sharepoint.md#fontSlot) in [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e837c-p109">Replace  _FontSlot_ with the name of the font slot to use. To see a list of available font slots, see the [Font slots](color-palettes-and-fonts-in-sharepoint.md#fontSlot) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="e837c-p110">Im Folgenden ist ein Beispiel der **ReplaceFont** -Anmerkung dargestellt. Wenn der **body**-Schriftartenplatz im Design als Courier definiert ist, wird Courier in diesem Beispiel als erstes Element zur Liste der verfügbaren Schriftarten des **Choose the Look**-Assistenten hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="e837c-p110">The following shows an example of the **ReplaceFont** annotation. In this example, if the **body** font slot is defined as Courier in the theme, Courier will be added as the first item in the list of available fonts in the **Choose the Look** wizard.</span></span>
  
    
    

-  `/* [ReplaceFont(themeFont:"body")] */ font-family:"Segoe UI","Segoe",Tahoma,Helvetica,Arial,sans-serif;`
    
  

### <a name="replacebgimage-annotation"></a><span data-ttu-id="e837c-143">ReplaceBGImage-Anmerkung</span><span class="sxs-lookup"><span data-stu-id="e837c-143">ReplaceBGImage annotation</span></span>
<span data-ttu-id="e837c-144"><a name="replaceBGimage"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-144"><a name="replaceBGimage"> </a></span></span>

<span data-ttu-id="e837c-p111">Die **ReplaceBGImage** -Anmerkung ersetzt das Hintergrundbild in der CSS-Datei durch das Designhintergrundbild. Sie kann mit den CSS-Eigenschaften **background** und **background-image** verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e837c-p111">The **ReplaceBGImage** annotation replaces the background image in the CSS file with the theme background image. It can be used with the **background** and **background-image** CSS properties.</span></span>
  
    
    
<span data-ttu-id="e837c-p112">Im Folgenden ist das Format für die **ReplaceBGImage** -Anmerkung dargestellt. Die **ReplaceBGImage** -Anmerkung kann auch mit dem **AlphaImageLoader**-Filter verwendet werden, um ältere Versionen von Internet Explorer zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="e837c-p112">The following shows the format for the **ReplaceBGImage** annotation. The **ReplaceBGImage** annotation can also be used with the **AlphaImageLoader** filter to support earlier versions of Internet Explorer.</span></span>
  
    
    



```
/* [ReplaceBGImage] */
```


### <a name="recolorimage-annotation"></a><span data-ttu-id="e837c-149">RecolorImage-Anmerkung</span><span class="sxs-lookup"><span data-stu-id="e837c-149">RecolorImage annotation</span></span>
<span data-ttu-id="e837c-150"><a name="replaceBGimage"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-150"><a name="replaceBGimage"> </a></span></span>

<span data-ttu-id="e837c-151">Die **RecolorImage** -Anmerkung färbt das angegebene Bild neu ein.</span><span class="sxs-lookup"><span data-stu-id="e837c-151">The **RecolorImage** annotation recolors the image specified.</span></span>
  
    
    
<span data-ttu-id="e837c-152">Im Folgenden wird das Format der **RecolorImage** -Anmerkung erläutert.</span><span class="sxs-lookup"><span data-stu-id="e837c-152">The following describes the format of the **RecolorImage** annotation.</span></span>
  
    
    



```
/* [RecolorImage(themeColor:"ColorSlot"[, method:["Tinting"|"Blending"|"Filling"]][, includeRectangle: {x:x-Setting,y:y-Setting,width:RegionWidth,height:RegionHeight})] */

```

<span data-ttu-id="e837c-p113">Ersetzen Sie  _ColorSlot_ durch den Anmerkungsnamen des Farbplatzes. Eine Liste der verfügbaren Farbplätze finden Sie im Abschnitt [Zuordnen von Farbplätzen](color-palettes-and-fonts-in-sharepoint.md#colorSlots) in [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="e837c-p113">Replace  _ColorSlot_ with the annotation name of the color slot. To see a list of available color slots, see the [Color slot mapping](color-palettes-and-fonts-in-sharepoint.md#colorSlots) section in [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
  
    
    
<span data-ttu-id="e837c-155">Verwenden Sie den optionalen **method** -Parameter, wenn Sie die Methode zum Neueinfärben angeben möchten.</span><span class="sxs-lookup"><span data-stu-id="e837c-155">Use the optional **method** parameter if you want to specify the recoloring method.</span></span>
  
    
    
<span data-ttu-id="e837c-p114">Verwenden Sie den optionalen **includeRectangle** -Parameter, wenn Sie nur einen bestimmten Bereich eines Bilds neu einfärben möchten. Ersetzen Sie _x-Setting_,  _y-Setting_,  _RegionWidth_ und _RegionHeight_ durch die X-Koordinate, die Y-Koordinate, die Breite und die Höhe des Bereichs, den Sie neu einfärben möchten.</span><span class="sxs-lookup"><span data-stu-id="e837c-p114">Use the optional **includeRectangle** parameter if you want to recolor only a specific region of an image. Replace _x-Setting_,  _y-Setting_,  _RegionWidth_, and  _RegionHeight_ with the x-coordinate, y-coordinate, width, and height of the region that you want to recolor.</span></span>
  
    
    
<span data-ttu-id="e837c-158">Im Folgenden finden Sie Beispiele zur Verwendung der **RecolorImage** -Anmerkung in einer CSS-Datei.</span><span class="sxs-lookup"><span data-stu-id="e837c-158">The following shows examples of the **RecolorImage** annotation being used in a CSS file.</span></span>
  
    
    

-  `/* [RecolorImage(themeColor:"SubtleBodyText",method:"Tinting")] */ background-image:url("/_layouts/15/images/tabtitlerowbottombg.png?rev=23");`
    
  
-  `/* [RecolorImage(themeColor:"BodyText",method:"Filling",includeRectangle:{x:161,y:178,width:16;height:16})] */ background:url("/_layouts/15/images/spcommon.png?rev=23") no-repeat -161px -178px;`
    
  

## <a name="upload-the-css-file-to-the-themable-folder-in-the-style-library"></a><span data-ttu-id="e837c-159">Hochladen der CSS-Datei in den Ordner "Themable" der Formatbibliothek</span><span class="sxs-lookup"><span data-stu-id="e837c-159">Upload the CSS file to the Themable folder in the Style library</span></span>
<span data-ttu-id="e837c-160"><a name="uploadCSS"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-160"><a name="uploadCSS"> </a></span></span>

<span data-ttu-id="e837c-p115">Legen Sie die benutzerdefinierten CSS-Dateien im Ordner "Themable" der Formatbibliothek ab (nicht im Ordner "Themable" des Gestaltungsvorlagenkatalogs). Das Designmodul erkennt nur CSS-Dateien, die im Ordner "Themable" der Formatbibliothek gespeichert sind. Der Ordner "Themable" wird für Veröffentlichungswebsites automatisch erstellt. Andernfalls können Sie den Ordner "Themable" auch am entsprechenden Speicherort (http://  _SiteCollectionName_/Style Library/ _language_/Themable/) erstellen.</span><span class="sxs-lookup"><span data-stu-id="e837c-p115">Place the custom CSS files in the Themable folder in the Style library (not the Themable folder in the Master Page Gallery). Only CSS files that are stored in the Themable folder in the Style library are recognized by the theming engine. The Themable folder is created automatically for publishing sites. Otherwise, you can create the Themable folder in the correct location (http://  _SiteCollectionName_/Style Library/ _language_/Themable/).</span></span>
  
    
    

> <span data-ttu-id="e837c-165">**Hinweis:** Der Name des _language_-Ordners muss im 4-stelligen Format _ll-cc_ angegeben sein, um die Sprache und die Kultur zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="e837c-165">**Note:** The name of the  _language_ folder must be in the 4-digit format _ll-cc_ to identify the language and culture, respectively.</span></span> <span data-ttu-id="e837c-166">Beispiel: en-us oder de-de.</span><span class="sxs-lookup"><span data-stu-id="e837c-166">For example, en-us or ar-sa.</span></span> <span data-ttu-id="e837c-167">Weitere Informationen finden Sie unter [Sprachen-IDs und ID-Werte für „OptionState“ in Office 2013](http://technet.microsoft.com/de-DE/library/cc179219.aspx).</span><span class="sxs-lookup"><span data-stu-id="e837c-167">For more information, see [Language identifiers and OptionState Id values in Office 2013](http://technet.microsoft.com/de-DE/library/cc179219.aspx).</span></span> 
  
    
    

<span data-ttu-id="e837c-p117">CSS-Dateien müssen eingecheckt und veröffentlicht werden. Wenn CSS-Dateien geändert werden, müssen Sie das Design erneut anwenden, damit die Änderungen erkannt werden.</span><span class="sxs-lookup"><span data-stu-id="e837c-p117">CSS files must be checked in and published. If CSS files are changed, you must reapply the theme for the changes to be recognized.</span></span>
  
    
    

## <a name="register-the-css-file"></a><span data-ttu-id="e837c-170">Registrieren der CSS-Datei</span><span class="sxs-lookup"><span data-stu-id="e837c-170">Register the CSS file</span></span>
<span data-ttu-id="e837c-171"><a name="registerCSS"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-171"><a name="registerCSS"> </a></span></span>

<span data-ttu-id="e837c-p118">Sie müssen die CSS-Datei bei einer Gestaltungsvorlage registrieren, bevor die CSS-Datei vom Designmodul verwendet werden kann. Dadurch wird die Gestaltungsvorlage zu der CSS-Datei geleitet, wenn Sie ein Design auf eine Website anwenden. Um eine CSS-Datei zu registrieren, müssen Sie ein **<SharePoint:CssRegistration>**-Element zum **<head>**-Element der Gestaltungsvorlage hinzufügen. Im Folgenden ist das Format des **<SharePoint:CssRegistration>**-Elements dargestellt.</span><span class="sxs-lookup"><span data-stu-id="e837c-p118">You must register the CSS file with a master page before the CSS file can be used by the theming engine. This directs the master page to the CSS file when you apply a theme to a site. To register a CSS file, you add a **<SharePoint:CssRegistration>** element to the **<head>** element of the master page. The following shows the format of the **<SharePoint:CssRegistration>** element.</span></span>
  
    
    

```HTML

<SharePoint:CssRegistration Name="CSSFileLocation" runat="server" />
```

<span data-ttu-id="e837c-176">Ersetzen Sie  _CSSFileLocation_ durch den Speicherort der CSS-Datei.</span><span class="sxs-lookup"><span data-stu-id="e837c-176">Replace  _CSSFileLocation_ with the location of the CSS file.</span></span>
  
    
    
<span data-ttu-id="e837c-177">Im Folgenden finden Sie ein Beispiel für ein **<SharePoint:CssRegistration>**-Element.</span><span class="sxs-lookup"><span data-stu-id="e837c-177">The following is an example of an **<SharePoint:CssRegistration>** element.</span></span>
  
    
    



```HTML
<head>
…
<SharePoint:CssRegistration Name="<%$SPUrl:~SiteCollection/Style Library/~language/Themable/MyCustomFile.css%>" runat="server" />
</head>
```


> <span data-ttu-id="e837c-178">**Hinweis:** Das Token **%$SPUrl** kann nicht in SharePoint Foundation 2013 verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e837c-178">**Note:** The **%$SPUrl** token cannot be used on SharePoint Foundation 2013.</span></span> <span data-ttu-id="e837c-179">Sie müssen eine URL verwenden, um den Speicherort der CSS-Datei anzugeben.</span><span class="sxs-lookup"><span data-stu-id="e837c-179">You must use a URL to specify the location of the CSS file.</span></span>
  
    
    


## <a name="additional-resources"></a><span data-ttu-id="e837c-180">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="e837c-180">Additional resources</span></span>
<span data-ttu-id="e837c-181"><a name="addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="e837c-181"><a name="addresources"> </a></span></span>


-  [<span data-ttu-id="e837c-182">Übersicht über Designs für SharePoint</span><span class="sxs-lookup"><span data-stu-id="e837c-182">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md)
    
  
-  [<span data-ttu-id="e837c-183">Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e837c-183">How to: Deploy a custom theme in SharePoint</span></span>](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e837c-184">Aktualisieren benutzerdefinierter Designs und CSS-Dateien auf SharePoint</span><span class="sxs-lookup"><span data-stu-id="e837c-184">Upgrade custom themes and CSS to SharePoint</span></span>](upgrade-custom-themes-and-css-to-sharepoint.md)
    
  
-  [<span data-ttu-id="e837c-185">Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e837c-185">How to: Create a master page preview file in SharePoint</span></span>](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e837c-186">Farbpaletten und Schriftarten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="e837c-186">Color palettes and fonts in SharePoint</span></span>](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="e837c-187">SharePoint-Teamblog: Beweisen Sie Stil mit SharePoint-Designs</span><span class="sxs-lookup"><span data-stu-id="e837c-187">SharePoint Team Blog: Show off your style with SharePoint theming</span></span>](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [<span data-ttu-id="e837c-188">SharePoint Design Manager - Branding- und Designfunktionen</span><span class="sxs-lookup"><span data-stu-id="e837c-188">SharePoint Design Manager branding and design capabilities</span></span>](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

