---
title: "Gewusst wie Benutzerdefinierte CSS-Dateien in SharePoint designfähig gestalten"
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: b8c82c77-c836-47f9-a11e-6c9c656d436b
ms.openlocfilehash: 24d22d47c8c53b0aeb33a14bef989ab3138a06f8
ms.sourcegitcommit: 1cae27d85ee691d976e2c085986466de088f526c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/13/2017
---
# <a name="how-to-make-custom-css-files-themable-in-sharepoint"></a>Gewusst wie: Benutzerdefinierte CSS-Dateien in SharePoint designfähig gestalten
Erfahren Sie mehr über das Hinzufügen von Kommentarstil-Markups zu einer CSS-Datei, sodass sie im SharePoint-Designmodul verwendet werden kann.
## <a name="introduction-to-annotations"></a>Einführung in Anmerkungen
<a name="Intro"> </a>

Anmerkungen sind spezielle Kommentarstil-Markups, die dem SharePoint-Designmodul mitteilen, wie die Eigenschaften in einer CSS-Datei gestaltet werden sollen. Wenn ein Design auf eine Website angewendet wird, ersetzt das Designmodul die CSS-Eigenschaftswerte durch die entsprechenden Designwerte. In SharePoint können Sie Anmerkungen verwenden, um die Farbe, die Schriftart oder das Hintergrundbild zu ändern. Sie können ein Bild auch neu einfärben. Bei Verwendung benutzerdefinierter CSS-Dateien müssen Sie diese Anmerkungen zu den CSS-Dateien hinzufügen, wenn Sie sie mit dem SharePoint-Designmodul verwenden möchten. Wenn Sie ein Design auf eine Website anwenden, die benutzerdefinierte CSS-Dateien verwendet, und Sie keine Anmerkungen hinzugefügt haben, bleiben die CSS-Eigenschaften unverändert. Das kann zu einem unstimmigen Design der Website führen.
  
    
    
In diesem Artikel werden die verfügbaren Anmerkungen und die Vorgehensweise zum Registrieren von CSS-Dateien beschrieben.
  
    
    
Weitere Informationen zu benutzerdefinierten Designs finden Sie unter  [Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md) und [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md).
  
    
    

## <a name="add-annotations-to-custom-css-files"></a>Hinzufügen von Anmerkungen zu benutzerdefinierten CSS-Dateien
<a name="annotations"> </a>

Anmerkungen teilen dem SharePoint-Designmodul mit, wie die Eigenschaften in einer CSS-Datei gestaltet werden sollen. In diesem Abschnitt werden die verfügbaren Anmerkungen und ihre Verwendungsweise erläutert.
  
    
    

### <a name="replacecolor-annotation"></a>ReplaceColor-Anmerkung
<a name="replaceColor"> </a>

Die **ReplaceColor** -Anmerkung ersetzt den Farbwert durch die angegebene Designfarbe. Sie kann mit CSS-Eigenschaften verwendet werden, die einen Farbwert definieren, wie z. B. **color**, **background-color**, **border** usw.
  
    
    
Im Folgenden ist das Format für die **ReplaceColor**-Anmerkung dargestellt.
  
    
    



```

/* [ReplaceColor(themeColor:"ColorSlot"[, themeShade:"ShadeValue"][, themeTint:"TintValue"][, opacity:"OpacityValue"])] */

```

Ersetzen Sie  _ColorSlot_ durch den Anmerkungsnamen des zu verwendenden Farbplatzes. Eine Liste der verfügbaren Farbplätze finden Sie im Abschnitt [Zuordnen von Farbplätzen](color-palettes-and-fonts-in-sharepoint.md#colorSlots) in [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).
  
    
    
Verwenden Sie den optionalen **themeShade** -Parameter, wenn Sie die Designfarbe abdunkeln möchten. Ersetzen Sie _ShadeValue_ durch einen numerischen Wert von 0,0 (keine Änderung) bis 1,0 (dunkelste Schattierung).
  
    
    
Verwenden Sie den optionalen **themeTint** -Parameter, wenn Sie die Designfarbe aufhellen möchten. Ersetzen Sie _TintValue_ durch einen numerischen Wert von 0,0 (keine Änderung) bis 1,0 (hellste Schattierung).
  
    
    
Verwenden Sie den optionalen **opacity** -Parameter, wenn Sie die Deckkraft der Designfarbe angeben möchten. Ersetzen Sie _OpacityValue_ durch einen numerischen Wert, der die Deckkrafteinstellung angibt. Der Bereich der Deckkrafteinstellung liegt zwischen 0,0 (vollständig transparent) und 1,0 (vollständig deckend).
  
    
    
Im Folgenden finden Sie Beispiele für die Verwendung der **ReplaceColor** -Anmerkung in einer CSS-Datei.
  
    
    

-  `/* [ReplaceColor(themeColor:"BodyText")] */ color:#444;`
    
  
-  `/* [ReplaceColor(themeColor:"BackgroundOverlay",opacity:"0.5")] */ background-color:#fff;`
    
  
-  `/* [ReplaceColor(themeColor:"EmphasisBackground",themeTint:"0.05")] */ background-color:#f2faff;`
    
  

### <a name="replacefont-annotation"></a>ReplaceFont-Anmerkung
<a name="replaceFont"> </a>

Die **ReplaceFont** -Anmerkung fügt die angegebene Designschriftfarbe zur Liste der verfügbaren Schriftarten hinzu. Sie kann mit den CSS-Eigenschaften **font** und **font-family** verwendet werden.
  
    
    
Im Folgenden ist das Format für die **ReplaceFont** -Anmerkung dargestellt.
  
    
    



```

/* [ReplaceFont(themeFont:"FontSlot")] */
```

Ersetzen Sie  _FontSlot_ durch den Namen des zu verwendenden Schriftartenplatzes. Eine Liste der verfügbaren Schriftartenplätze finden Sie im Abschnitt [Schriftartenplätze](color-palettes-and-fonts-in-sharepoint.md#fontSlot) in [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).
  
    
    
Im Folgenden ist ein Beispiel der **ReplaceFont** -Anmerkung dargestellt. Wenn der **body**-Schriftartenplatz im Design als Courier definiert ist, wird Courier in diesem Beispiel als erstes Element zur Liste der verfügbaren Schriftarten des **Choose the Look**-Assistenten hinzugefügt.
  
    
    

-  `/* [ReplaceFont(themeFont:"body")] */ font-family:"Segoe UI","Segoe",Tahoma,Helvetica,Arial,sans-serif;`
    
  

### <a name="replacebgimage-annotation"></a>ReplaceBGImage-Anmerkung
<a name="replaceBGimage"> </a>

Die **ReplaceBGImage** -Anmerkung ersetzt das Hintergrundbild in der CSS-Datei durch das Designhintergrundbild. Sie kann mit den CSS-Eigenschaften **background** und **background-image** verwendet werden.
  
    
    
Im Folgenden ist das Format für die **ReplaceBGImage** -Anmerkung dargestellt. Die **ReplaceBGImage** -Anmerkung kann auch mit dem **AlphaImageLoader**-Filter verwendet werden, um ältere Versionen von Internet Explorer zu unterstützen.
  
    
    



```
/* [ReplaceBGImage] */
```


### <a name="recolorimage-annotation"></a>RecolorImage-Anmerkung
<a name="replaceBGimage"> </a>

Die **RecolorImage** -Anmerkung färbt das angegebene Bild neu ein.
  
    
    
Im Folgenden wird das Format der **RecolorImage** -Anmerkung erläutert.
  
    
    



```
/* [RecolorImage(themeColor:"ColorSlot"[, method:["Tinting"|"Blending"|"Filling"]][, includeRectangle: {x:x-Setting,y:y-Setting,width:RegionWidth,height:RegionHeight})] */

```

Ersetzen Sie  _ColorSlot_ durch den Anmerkungsnamen des Farbplatzes. Eine Liste der verfügbaren Farbplätze finden Sie im Abschnitt [Zuordnen von Farbplätzen](color-palettes-and-fonts-in-sharepoint.md#colorSlots) in [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).
  
    
    
Verwenden Sie den optionalen **method** -Parameter, wenn Sie die Methode zum Neueinfärben angeben möchten.
  
    
    
Verwenden Sie den optionalen **includeRectangle** -Parameter, wenn Sie nur einen bestimmten Bereich eines Bilds neu einfärben möchten. Ersetzen Sie _x-Setting_,  _y-Setting_,  _RegionWidth_ und _RegionHeight_ durch die X-Koordinate, die Y-Koordinate, die Breite und die Höhe des Bereichs, den Sie neu einfärben möchten.
  
    
    
Im Folgenden finden Sie Beispiele zur Verwendung der **RecolorImage** -Anmerkung in einer CSS-Datei.
  
    
    

-  `/* [RecolorImage(themeColor:"SubtleBodyText",method:"Tinting")] */ background-image:url("/_layouts/15/images/tabtitlerowbottombg.png?rev=23");`
    
  
-  `/* [RecolorImage(themeColor:"BodyText",method:"Filling",includeRectangle:{x:161,y:178,width:16;height:16})] */ background:url("/_layouts/15/images/spcommon.png?rev=23") no-repeat -161px -178px;`
    
  

## <a name="upload-the-css-file-to-the-themable-folder-in-the-style-library"></a>Hochladen der CSS-Datei in den Ordner "Themable" der Formatbibliothek
<a name="uploadCSS"> </a>

Legen Sie die benutzerdefinierten CSS-Dateien im Ordner "Themable" der Formatbibliothek ab (nicht im Ordner "Themable" des Gestaltungsvorlagenkatalogs). Das Designmodul erkennt nur CSS-Dateien, die im Ordner "Themable" der Formatbibliothek gespeichert sind. Der Ordner "Themable" wird für Veröffentlichungswebsites automatisch erstellt. Andernfalls können Sie den Ordner "Themable" auch am entsprechenden Speicherort (http://  _SiteCollectionName_/Style Library/ _language_/Themable/) erstellen.
  
    
    

> **Hinweis:** Der Name des _language_-Ordners muss im 4-stelligen Format _ll-cc_ angegeben sein, um die Sprache und die Kultur zu identifizieren. Beispiel: en-us oder de-de. Weitere Informationen finden Sie unter [Sprachen-IDs und ID-Werte für „OptionState“ in Office 2013](http://technet.microsoft.com/en-us/library/cc179219.aspx). 
  
    
    

CSS-Dateien müssen eingecheckt und veröffentlicht werden. Wenn CSS-Dateien geändert werden, müssen Sie das Design erneut anwenden, damit die Änderungen erkannt werden.
  
    
    

## <a name="register-the-css-file"></a>Registrieren der CSS-Datei
<a name="registerCSS"> </a>

Sie müssen die CSS-Datei bei einer Gestaltungsvorlage registrieren, bevor die CSS-Datei vom Designmodul verwendet werden kann. Dadurch wird die Gestaltungsvorlage zu der CSS-Datei geleitet, wenn Sie ein Design auf eine Website anwenden. Um eine CSS-Datei zu registrieren, müssen Sie ein **<SharePoint:CssRegistration>**-Element zum **<head>**-Element der Gestaltungsvorlage hinzufügen. Im Folgenden ist das Format des **<SharePoint:CssRegistration>**-Elements dargestellt.
  
    
    

```HTML

<SharePoint:CssRegistration Name="CSSFileLocation" runat="server" />
```

Ersetzen Sie  _CSSFileLocation_ durch den Speicherort der CSS-Datei.
  
    
    
Im Folgenden finden Sie ein Beispiel für ein **<SharePoint:CssRegistration>**-Element.
  
    
    



```HTML
<head>
…
<SharePoint:CssRegistration Name="<%$SPUrl:~SiteCollection/Style Library/~language/Themable/MyCustomFile.css%>" runat="server" />
</head>
```


> **Hinweis:** Das Token **%$SPUrl** kann nicht in SharePoint Foundation 2013 verwendet werden. Sie müssen eine URL verwenden, um den Speicherort der CSS-Datei anzugeben.
  
    
    


## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="addresources"> </a>


-  [Übersicht über Designs für SharePoint](themes-overview-for-sharepoint.md)
    
  
-  [Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [Aktualisieren benutzerdefinierter Designs und CSS-Dateien auf SharePoint](upgrade-custom-themes-and-css-to-sharepoint.md)
    
  
-  [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [SharePoint-Teamblog: Beweisen Sie Stil mit SharePoint-Designs](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [SharePoint Design Manager - Branding- und Designfunktionen](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

