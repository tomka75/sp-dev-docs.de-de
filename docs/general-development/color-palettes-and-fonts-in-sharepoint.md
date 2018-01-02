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
# <a name="color-palettes-and-fonts-in-sharepoint"></a>Farbpaletten und Schriftarten in SharePoint
Verwenden Sie diese Übersicht, um die in einer SharePoint-Website verwendeten Farbpaletten oder Schriftartenschemas zu definieren.
## <a name="color-palettes"></a>Farbpaletten
<a name="color"> </a>

Eine Farbpalette stellt die Kombination der Farben dar, die in einer SharePoint-Website verwendet werden. Die Farbpalette für eine SharePoint-Website wird in einer Farbpalettendatei definiert. Farbplätze werden auch von der Vorschaudatei für Gestaltungsvorlagen verwendet, um Miniatur- und Vorschaubilder einer Website zu erstellen. Im Folgenden wird der Aufbau der Farbpalettendatei und der Vorschaudatei für Gestaltungsvorlagen beschrieben:
  
    
    

- **Farbpalettendatei (.spcolor)**
    
    Farbpalettendateien werden im Assistenten **Aussehen ändern** verwendet, mit dem Benutzer das Erscheinungsbild ihrer Website mithilfe der SharePoint-Designbenutzeroberfläche ändern können. Mit SharePoint werden standardmäßig 32 Farbpalettendateien installiert. Sie können auch zusätzliche Farbpalettendateien erstellen. Das folgende Beispiel zeigt das Format einer Farbpalettendatei.
    

```xml  
<s:colorPalette isInverted="InvertedSetting" previewSlot1="Slot1" previewSlot2="Slot2" previewSlot3="Slot3" xmlns:s="http://schemas.microsoft.com/sharepoint/">
    <s:color name="ColorSlot" value="Color" />
    <!--additional color slots-->
</s:colorPalette>
```


  In einer Farbpalettendatei werden die folgenden Platzhalter ersetzt:
    
-  _InvertedSetting_ ist ein Boolescher Wert. **true**, wenn die Farbpalette in der Regel hellen Text vor dunklem Hintergrund umfasst. **false**, wenn die Farbpalette in der Regel dunklen Text vor hellem Hintergrund umfasst.
    
  
-  _Slot1_ ist der Anmerkungsname des Farbplatzes, der in der Farbpalettenauswahl der Designoberfläche als der erste Block des Palettensymbols verwendet werden soll.
    
  
-  _Slot2_ ist der Anmerkungsname des Farbplatzes, der in der Farbpalettenauswahl der Designoberfläche als der zweite Block des Palettensymbols verwendet werden soll.
    
  
-  _Slot3_ ist der Anmerkungsname des Farbplatzes, der in der Farbpalettenauswahl der Designoberfläche als der dritte Block des Palettensymbols verwendet werden soll.
    
  
-  _ColorSlot_ ist der Anmerkungsname des Farbplatzes, den Sie definieren (z. B. Websitetitel).
    
  
-  _Color_ ist der Hexadezimalwert der Farbe, die für den angegebenen Farbplatz verwendet werden soll. Er kann sechsstellig (RRGGBB) oder achtstellig (AARRGGBB) sein. Wenn der Hexadezimalwert achtstellig ist, geben die ersten beiden Stellen die Transparenzstufe (00-FF, was 0-255 entspricht) an. Ist der Hexadezimalwert sechsstellig, ist der Standardtransparenzwert 100 % oder FF.
    
  

  Die Farbpalettendateien sich im Designkatalog der Stammwebsite gespeichert, in der Websitesammlung im Ordner **15** (http:// _SiteCollectionName_/_catalogs/theme/15/). Um den Designkatalog über die Benutzerfläche von SharePoint aufzurufen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** **Designs** und dann **15** aus.
    
  
- **Vorschaudatei für Gestaltungsvorlagen (.preview)**
    
  Vorschaudateien für Gestaltungsvorlagen werden verwendet, um bei Verwendung des Assistenten **Aussehen ändern** Miniatur- und Vorschaubilder zu generieren. Eine Gestaltungsvorlage muss eine entsprechende Vorschaudatei aufweisen, die im Assistenten **Aussehen ändern** verwendet wird. Eine Vorschaudatei stellt eine speziell formatierte Datei dar, die Abschnitte für die Standardfarbpalette, das Standardschriftartenschema, Token-CSS und Token-HTML enthält. Sie verwendet Zeichenfolgetoken, um den Wert von Farbplätzen, Schriftartnamen und lokalisierten UI-Zeichenfolgen abzurufen. Das folgende Beispiel zeigt Farbplätze, die in der Vorschaudatei für Gestaltungsvorlagen verwendet werden.
    


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


  Weitere Informationen finden Sie unter [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  

> **Tipp:** Sie können das SharePoint-Farbpalettentool zum Erstellen von SharePoint-Designs verwenden. Sie können [das SharePoint-Farbpalettentool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) im Microsoft Download Center herunterladen.
  
    
    


### <a name="color-slot-mapping"></a>Farbmodul-Zuordnung
<a name="colorSlots"> </a>

Tabelle 1 beschreibt die verfügbaren Farbmodule und wo diese Farbmodule auf einer SharePoint-Website verwendet werden.
  
> [!NOTE]
> Bei der Erläuterung von Navigationselementen bedeutet „Pressed“ (Gedrückt), dass ein Benutzer auf ein Navigationselement klickt oder es berührt. „Selected“ (Ausgewählt) bezieht sich darauf, dass ein Benutzer auf die Seite geleitet wird.> Nachfolgend finden Sie eine Zusammenfassung einer normalen Aktionenfolge und des Farbmoduls für den Navigationselement-Link in jedem Schritt:> Der Basistext eines Navigationselement-Links: HeaderNavigationText> Ein Benutzer bewegt den Cursor über den Navigationselement-Link: HeaderNavigationHoverText> Ein Benutzer klickt auf, berührt oder wählt den Navigationselement-Link: HeaderNavigationPressedText> Der Benutzer wird auf die ausgewählten Seite geleitet. Das Farbmodul, das sich auf das Navigationselement für die Seite bezieht, auf der sich der Benutzer nun befindet: HeaderNavigationSelectedText
  
    
    


**Tabelle 1. Farbmodule**


|**Anmerkungsname**|**Wo die Farbe in der UI verwendet wird**|**Tokenname**|
|:-----|:-----|:-----|
|BodyText  <br/> |Normaler Textkörper  <br/> |[T_THEME_COLOR_BODYTEXT]  <br/> |
|SubtleBodyText  <br/> |Textkörper, der heller als normal sein muss, wie z. B. Metadatentext  <br/> |[T_THEME_COLOR_SUBTLEBODYTEXT]  <br/> |
|StrongBodyText  <br/> |Textkörperfarbe für Text, der sich vom normalen Textkörper abheben muss  <br/> |[T_THEME_COLOR_STRONGBODYTEXT]  <br/> |
|DisabledText  <br/> |Deaktivierter Text, z. B. nicht verfügbare Elemente in Menüs  <br/> |[T_THEME_COLOR_DISABLEDTEXT]  <br/> |
|SiteTitle  <br/> |Die Textfarbe des Seitentitels  <br/> |[T_THEME_COLOR_SITETITLE]  <br/> |
|WebPartHeading  <br/> |Textfarbe für Webpart-Überschriften  <br/> |[T_THEME_COLOR_WEBPARTHEADING]  <br/> |
|ErrorText  <br/> |Die Hauptfarbe für Text, Rahmen und Hintergründe, die sich auf Fehler beziehen (nach Bedarf)  <br/> |[T_THEME_COLOR_ERRORTEXT]  <br/> |
|AccentText  <br/> |Textfarbe für hervorgehobenen Textkörper  <br/> |[T_THEME_COLOR_ACCENTTEXT]  <br/> |
|SearchURL  <br/> |Textfarbe für die in Suchergebnissen gefundene URL. Wird auch zum Hervorheben neuer Elemente oder Erfolgsstatusmeldungen verwendet.  <br/> |[T_THEME_COLOR_SEARCHURL]  <br/> |
|Hyperlink  <br/> |Textfarbe für Hyperlinks  <br/> |[T_THEME_COLOR_HYPERLINK]  <br/> |
|HyperlinkFollowed  <br/> |Textfarbe für gefolgte Hyperlinks  <br/> |[T_THEME_COLOR_HYPERLINKFOLLOWED]  <br/> |
|HyperlinkActive  <br/> |Hyperlinkfarbe, wenn Hyperlink gedrückt wird  <br/> |[T_THEME_COLOR_HYPERLINKACTIVE]  <br/> |
|CommandLinks  <br/> |Große Befehlslinks, die aufgrund ihrer Größe ein bisschen heller sein müssen als der Textkörper  <br/> |[T_THEME_COLOR_COMMANDLINKS]  <br/> |
|CommandLinksSecondary  <br/> |Befehlslinkfarbe für Links, die kleiner sind und daher eine stärkere Farbe aufweisen, um hervorzutreten  <br/> |[T_THEME_COLOR_COMMANDLINKSSECONDARY]  <br/> |
|CommandLinksHover  <br/> |Befehlslinkfarbe beim Daraufzeigen  <br/> |[T_THEME_COLOR_COMMANDLINKSHOVER]  <br/> |
|CommandLinksPressed  <br/> |Befehlslinkfarbe, wenn Befehlslink gedrückt wird  <br/> |[T_THEME_COLOR_COMMANDLINKSPRESSED]  <br/> |
|CommandLinksDisabled  <br/> |Befehlslinkfarbe, wenn Befehlslink deaktiviert ist  <br/> |[T_THEME_COLOR_COMMANDLINKSDISABLED]  <br/> |
|BackgroundOverlay  <br/> |Die Haupthintergrundfarbe, die zwischen dem optionalen Hintergrundbild und dem Seiteninhalt sichtbar ist  <br/> |[T_THEME_COLOR_BACKGROUNDOVERLAY]  <br/> |
|DisabledBackground  <br/> |Hintergrund für deaktivierte Elemente wie Browsersteuerelemente, z. B. Eingabe- oder Auswahlfeld (außer Schaltflächen)  <br/> |[T_THEME_COLOR_DISABLEDBACKGROUND]  <br/> |
|PageBackground  <br/> |Die Hintergrundfarbe der Seite. Erscheint hinter dem optionalen Hintergrundbild.  <br/> |[T_THEME_COLOR_PAGEBACKGROUND]  <br/> |
|HeaderBackground  <br/> |Die Hintergrundfarbe für den Kopfbereich der Seite  <br/> |[T_THEME_COLOR_HEADERBACKGROUND]  <br/> |
|FooterBackground  <br/> |Die Hintergrundfarbe für den Fußzeilenbereich der Seite  <br/> |[T_THEME_COLOR_FOOTERBACKGROUND]  <br/> |
|SelectionBackground  <br/> |Die Hintergrundfarbe für ausgewählte Listenelemente und Dropdownmenü-Elemente  <br/> |[T_THEME_COLOR_SELECTIONBACKGROUND]  <br/> |
|HoverBackground  <br/> |Die Hintergrundfarbe für Listenelemente und Dropdownmenü-Elemente beim Daraufzeigen  <br/> |[T_THEME_COLOR_HOVERBACKGROUND]  <br/> |
|RowAccent  <br/> |Der hervorgehobene linke Rand bei ausgewählten Listenelementen  <br/> |[T_THEME_COLOR_ROWACCENT]  <br/> |
|StrongLines  <br/> |Rahmen für Browsersteuerelemente beim Daraufzeigen  <br/> |[T_THEME_COLOR_STRONGLINES]  <br/> |
|Lines  <br/> |Rahmen für Browsersteuerelemente  <br/> |[T_THEME_COLOR_LINES]  <br/> |
|SubtleLines  <br/> |Farbe für dezente Rahmen, z. B. Rasterlinien für Inlinebearbeitung  <br/> |[T_THEME_COLOR_SUBTLELINES]  <br/> |
|DisabledLines  <br/> |Rahmenfarbe für deaktivierte Browsersteuerelemente wie Eingabe- und Auswahlfelder  <br/> |[T_THEME_COLOR_DISABLEDLINES]  <br/> |
|AccentLines  <br/> |Farbe für fokussierte Rahmen bei ausgewählten Browsersteuerelementen  <br/> |[T_THEME_COLOR_ACCENTLINES]  <br/> |
|DialogBorder  <br/> |Farbe für Dialogfeldrahmen  <br/> |[T_THEME_COLOR_DIALOGBORDER]  <br/> |
|Navigation  <br/> |Textfarbe für horizontale und vertikale Navigationselemente  <br/> |[T_THEME_COLOR_NAVIGATION]  <br/> |
|NavigationAccent  <br/> |Textfarbe für ein ausgewähltes horizontales Navigationselement  <br/> |[T_THEME_COLOR_NAVIGATIONACCENT]  <br/> |
|NavigationHover  <br/> |Navigationstextfarbe beim Daraufzeigen. Gilt für obere Navigationselemente und für Schnellstartelemente im horizontalen Modus  <br/> |[T_THEME_COLOR_NAVIGATIONHOVER]  <br/> |
|NavigationPressed  <br/> |Textfarbe von Navigationselementen, wenn diese gedrückt werden. Gilt für obere Navigationselemente und für Schnellstartelemente im horizontalen Modus  <br/> |[T_THEME_COLOR_NAVIGATIONPRESSED]  <br/> |
|NavigationHoverBackground  <br/> |Hintergrundfarbe für Schnellstartelemente im vertikalen Modus beim Daraufzeigen  <br/> |[T_THEME_COLOR_NAVIGATIONHOVERBACKGROUND]  <br/> |
|NavigationSelectedBackground  <br/> |Hintergrundfarbe von Schnellstartelementen im vertikalen Modus, nachdem das Navigationselement ausgewählt wurde  <br/> |[T_THEME_COLOR_NAVIGATIONSELECTEDBACKGROUND]  <br/> |
|EmphasisText  <br/> |Die Textfarbe, die auf hervorgehobenem Hintergrund angezeigt wird  <br/> |[T_THEME_COLOR_EMPHASISTEXT]  <br/> |
|EmphasisBackground  <br/> |Die Farbe für hervorgehobenen Hintergrund, der direkt hinter hervorgehobenem Text angezeigt wird  <br/> |[T_THEME_COLOR_EMPHASISBACKGROUND]  <br/> |
|EmphasisHoverBackground  <br/> |Hintergrundfarbe beim Daraufzeigen, für Elemente, die hervorgehobenen Hintergrund verwenden  <br/> |[T_THEME_COLOR_EMPHASISHOVERBACKGROUND]  <br/> |
|EmphasisBorder  <br/> |Rahmenfarbe für Elemente mit hervorgehobenem Hintergrund  <br/> |[T_THEME_COLOR_EMPHASISBORDER]  <br/> |
|EmphasisHoverBorder  <br/> |Rahmenfarbe beim Daraufzeigen für Elemente mit hervorgehobenem Hintergrund  <br/> |[T_THEME_COLOR_EMPHASISHOVERBORDER]  <br/> |
|SubtleEmphasisText  <br/> |Text, der auf dezent hervorgehobenem Hintergrund angezeigt wird  <br/> |[T_THEME_COLOR_SUBTLEEMPHASISTEXT]  <br/> |
|SubtleEmphasisCommandLinks  <br/> |Befehlslinkfarbe für Links, die auf dezent hervorgehobenem Hintergrund angezeigt werden  <br/> |[T_THEME_COLOR_SUBTLEEMPHASISCOMMANDLINKS]  <br/> |
|SubtleEmphasisBackground  <br/> |Hintergrund, der direkt hinter dezent hervorgehobenem Text angezeigt wird  <br/> |[T_THEME_COLOR_SUBTLEEMPHASISBACKGROUND]  <br/> |
|TopBarText  <br/> |Text- und Glyphenfarbe für das Willkommensmenü, Symbole auf der Schnellzugriffsleiste und geschlossene Registerkarten auf dem Menüband  <br/> |[T_THEME_COLOR_TOPBARTEXT]  <br/> |
|TopBarBackground  <br/> |Die Hintergrundfarbe für die obere Leiste, die unterhalb und rechts der Suitenavigation angezeigt wird  <br/> |[T_THEME_COLOR_TOPBARBACKGROUND]  <br/> |
|TopBarHoverText  <br/> |Text- und Glyphenfarbe beim Daraufzeigen für das Willkommensmenü, Symbole auf der Schnellzugriffsleiste und geschlossene Registerkarten auf dem Menüband  <br/> |[T_THEME_COLOR_TOPBARHOVERTEXT]  <br/> |
|TopBarPressedText  <br/> |Text- und Glyphenfarbe beim Drücken auf das Willkommensmenü, Symbole auf der Schnellzugriffsleiste und geschlossene Registerkarten auf dem Menüband  <br/> |[T_THEME_COLOR_TOPBARPRESSEDTEXT]  <br/> |
|HeaderText  <br/> |Die Basistextfarbe für den gesamten Kopfbereich  <br/> |[T_THEME_COLOR_HEADERTEXT]  <br/> |
|HeaderSubtleText  <br/> |Hilfetext für das Suchfeld im Kopfbereich  <br/> |[T_THEME_COLOR_HEADERSUBTLETEXT]  <br/> |
|HeaderDisableText  <br/> |Text für das Suchfeld, wenn sich das Suchfeld im Kopfbereich befindet und deaktiviert ist  <br/> |[T_THEME_COLOR_HEADERDISABLETEXT]  <br/> |
|HeaderNavigationText  <br/> |Basistextfarbe für Navigationslinks im Kopfbereich  <br/> |[T_THEME_COLOR_HEADERNAVIGATIONTEXT]  <br/> |
|HeaderNavigationHoverText  <br/> |Textfarbe für Navigationslinks im Kopfbereich beim Daraufzeigen auf den Link  <br/> |[T_THEME_COLOR_HEADERNAVIGATIONHOVERTEXT]  <br/> |
|HeaderNavigationPressedText  <br/> |Textfarbe für Navigationlinks im Kopfbereich beim Drücken des Links  <br/> |[T_THEME_COLOR_HEADERNAVIGATIONPRESSEDTEXT]  <br/> |
|HeaderNavigationSelectedText  <br/> |Textfarbe für Navigationslinks im Kopfbereich bei Auswahl des Links  <br/> |[T_THEME_COLOR_HEADERNAVIGATIONSELECTEDTEXT]  <br/> |
|HeaderLines  <br/> |Suchfeldlinien, wenn sich das Suchfeld im Kopfbereich befindet  <br/> |[T_THEME_COLOR_HEADERLINES]  <br/> |
|HeaderStrongLines  <br/> |Suchfeldlinien beim Daraufzeigen, wenn sich das Suchfeld im Kopfbereich befindet  <br/> |[T_THEME_COLOR_HEADERSTRONGLINES]  <br/> |
|HeaderAccentLines  <br/> |Suchfeldlinien im Fokus, wenn sich das Suchfeld im Kopfbereich befindet  <br/> |[T_THEME_COLOR_HEADERACCENTLINES]  <br/> |
|HeaderSublteLines  <br/> |Dezente Linien im Kopfbereich. Werden in CSS-Standarddateien nicht verwendet.  <br/> |[T_THEME_COLOR_HEADERSUBTLELINES]  <br/> |
|HeaderDisabledLines  <br/> |Suchfeldlinien, wenn sich das Suchfeld im Kopfbereich befindet und deaktiviert ist  <br/> |[T_THEME_COLOR_HEADERDISABLEDLINES]  <br/> |
|HeaderDisabledBackground  <br/> |Suchfeldhintergrund, wenn sich das Suchfeld im Kopfbereich befindet und deaktiviert ist  <br/> |[T_THEME_COLOR_HEADERDISABLEDBACKGROUND]  <br/> |
|HeaderFlyoutBorder  <br/> |Rahmen für Dropdownmenüs im Kopfbereich  <br/> |[T_THEME_COLOR_HEADERFLYOUTBORDER]  <br/> |
|HeaderSiteTitle  <br/> |Textfarbe für den Websitetitel im Kopfbereich  <br/> |[T_THEME_COLOR_HEADERSITETITLE]  <br/> |
|SuiteBarBackground  <br/> |Hintergrundfarbe für die Suitenavigation  <br/> |[T_THEME_COLOR_SUITEBARBACKGROUND]  <br/> |
|SuiteBarHoverBackground  <br/> |Hintergrundfarbe beim Daraufzeigen für die Suitenavigation  <br/> |[T_THEME_COLOR_SUITEBARHOVERBACKGROUND]  <br/> |
|SuiteBarText  <br/> |Text- und Glyphenfarbe für die Suitenavigationselemente  <br/> |[T_THEME_COLOR_SUITEBARTEXT]  <br/> |
|SuiteBarDisabledText  <br/> |Text- und Glyphenfarbe für deaktivierte Suiteelemente. Wird in CSS-Standarddateien nicht verwendet.  <br/> |[T_THEME_COLOR_SUITEBARDISABLEDTEXT]  <br/> |
|ButtonText  <br/> |Textfarbe für Schaltflächen  <br/> |[T_THEME_COLOR_BUTTONTEXT]  <br/> |
|ButtonDisabledText  <br/> |Textfarbe für deaktivierte Schaltflächen  <br/> |[T_THEME_COLOR_BUTTONDISABLEDTEXT]  <br/> |
|ButtonBackground  <br/> |Hintergrundfarbe für Schaltflächen  <br/> |[T_THEME_COLOR_BUTTONBACKGROUND]  <br/> |
|ButtonHoverBackground  <br/> |Hintergrundfarbe für Schaltflächen beim Daraufzeigen  <br/> |[T_THEME_COLOR_BUTTONHOVERBACKGROUND]  <br/> |
|ButtonPressedBackground  <br/> |Hintergrundfarbe für gedrückte Schaltflächen  <br/> |[T_THEME_COLOR_BUTTONPRESSEDBACKGROUND]  <br/> |
|ButtonDisabledBackground  <br/> |Hintergrundfarbe für deaktivierte Schaltflächen  <br/> |[T_THEME_COLOR_BUTTONDISABLEDBACKGROUND]  <br/> |
|ButtonBorder  <br/> |Rahmenfarbe für Schaltflächen  <br/> |[T_THEME_COLOR_BUTTONBORDER]  <br/> |
|ButtonHoverBorder  <br/> |Rahmenfarbe für Schaltflächen beim Daraufzeigen  <br/> |[T_THEME_COLOR_BUTTONHOVERBORDER]  <br/> |
|ButtonPressedBorder  <br/> |Rahmenfarbe für gedrückte Schaltflächen  <br/> |[T_THEME_COLOR_BUTTONPRESSEDBORDER]  <br/> |
|ButtonDisabledBorder  <br/> |Rahmenfarbe für Schaltflächen, die deaktiviert sind  <br/> |[T_THEME_COLOR_BUTTONDISABLEDBORDER]  <br/> |
|ButtonGlyph  <br/> |Glyphenfarbe für eine Glyphe, die in einer Schaltfläche angezeigt wird  <br/> |[T_THEME_COLOR_BUTTONGLYPH]  <br/> |
|ButtonGlyphActive  <br/> |Glyphenfarbe beim Daraufzeigen, für eine Glyphe, die in einer Schaltfläche angezeigt wird  <br/> |[T_THEME_COLOR_BUTTONGLYPHACTIVE]  <br/> |
|ButtonGlyphDisabled  <br/> |Glyphenfarbe für eine deaktivierte Schaltfläche  <br/> |[T_THEME_COLOR_BUTTONGLYPHDISABLED]  <br/> |
|TileText  <br/> |Der Text, der auf überlagertem Kachelhintergrund angezeigt wird  <br/> |[T_THEME_COLOR_TILETEXT]  <br/> |
|TileBackgroundOverlay  <br/> |Die Hintergrundüberlagerungsfarbe für Kacheln  <br/> |[T_THEME_COLOR_TILEBACKGROUNDOVERLAY]  <br/> |
|ContentAccent1  <br/> |Die erste Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann  <br/> |[T_THEME_COLOR_CONTENTACCENT1]  <br/> |
|ContentAccent2  <br/> |Die zweite Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann  <br/> |[T_THEME_COLOR_CONTENTACCENT2]  <br/> |
|ContentAccent3  <br/> |Die dritte Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann  <br/> |[T_THEME_COLOR_CONTENTACCENT3]  <br/> |
|ContentAccent4  <br/> |Die vierte Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann  <br/> |[T_THEME_COLOR_CONTENTACCENT4]  <br/> |
|ContentAccent5  <br/> |Die fünfte Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann  <br/> |[T_THEME_COLOR_CONTENTACCENT5]  <br/> |
|ContentAccent6  <br/> |Die sechste Akzentfarbe, die ein Benutzer in der Rich-Text-Editor-Farbauswahl auswählen kann  <br/> |[T_THEME_COLOR_CONTENTACCENT6]  <br/> |
   

## <a name="font-schemes"></a>Schriftartenschema
<a name="font"> </a>

Schriftarten werden im Schriftartenschema (.spfont-Datei) und der Gestaltungsvorlagenvorschau (.preview-Datei) für eine bestimmte SharePoint-Website definiert. Das Schriftartenschema definiert die Schriftarten, die in vier Bereichen verwendet werden: Titel, Navigation, Überschrift und Textkörper. Sieben Schriftartenschemas sind in SharePoint enthalten. Sie können zusätzliche Schriftartenschemas erstellen. Die Schriftartenschemadateien sind im **15**-Unterordner des Designkatalogs der Stammwebsite der Websitesammlung abgelegt (http:// _SiteCollectionName_/_catalogs/theme/15/). Um den Designkatalog über die Benutzerfläche von SharePoint aufzurufen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** **Designs** und dann **15** aus.
  
    
    
Das folgende Beispiel beschreibt das Format für eine .spfont-Datei.
  
    
    



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

In einer .spfont-Datei werden die folgenden Platzhalter ersetzt:
  
    
    

-  _FontSchemeName_ ist der Name des Schriftartenschemas.
    
  
-  _Slot1_ ist der Name des Schriftartenplatzes, den Sie als den ersten Block des Schriftartensymbols in der Schriftartenschemaauswahl im Assistenten **Aussehen ändern** verwenden möchten.
    
  
-  _Slot2_ ist der Name des Schriftartenplatzes, den Sie als den zweiten Block des Schriftartensymbols in der Schriftartenschemaauswahl im Assistenten **Aussehen ändern** verwenden möchten.
    
  
-  _FontSlotName_ ist der Name des Schriftartenplatzes, den Sie definieren (z. B. Titel).
    
  
-  _LatinScriptFont_ ist die Schriftart, die für lateinische Skripts verwendet werden soll. Diese Schriftart ist ebenfalls die Fallbackschriftart. Das bedeutet, dass diese Schriftart für eine Sprache verwendet wird, die kein im Schriftartenschema explizit festgelegtes Skript aufweist.
    
    > [!NOTE]
    > Sie müssen zusätzliche Informationen bereitstellen, wenn Sie Webschriftarten in Ihrem Schriftartenschema verwenden möchten. Weitere Informationen finden Sie im Abschnitt [Webschriftarten](#webFont) dieses Artikels.
-  _EAScriptFont_ ist die Schriftart, die für ostasiatische Skripts verwendet werden soll. Das **<s:ea>**-Element wird von SharePoint derzeit nicht verwendet. Das **<s:ea>**-Element wird im Schriftartenschema dennoch benötigt.
    
  
-  _CSFont_ ist die Schriftart, die für komplexe Skripts verwendet werden soll. Das **<s:cs>**-Element wird von SharePoint derzeit nicht verwendet. Das **<s:cs>**-Element wird im Schriftartenschema dennoch benötigt.
    
  
-  _Language_ ist das Sprachenskript.
    
  
-  _ScriptFont_ ist die Schriftart, die für das angegebene Sprachenskript verwendet werden soll.
    
  
Das folgende Beispiel zeigt einen Teil einer .spfont-Datei.
  
    
    



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

SharePoint umfasst Unterstützung für Webschriftarten. Sie müssen zusätzliche Informationen angeben, um in Ihrem Schriftartenschema Webschriftarten zu verwenden. Weitere Informationen finden Sie unter in diesem Artikel im Abschnitt  [Webschriftarten](#webFont).
  
    
    

### <a name="web-safe-fonts"></a>Websichere Schriftarten
<a name="websafeFont"> </a>

Als websichere Schriftarten werden Schriftarten bezeichnet, die häufig verwendet werden und auf den meisten Geräten standardmäßig verfügbar sind. Um im Schriftartenschema eine websichere Schriftart anzugeben, schließen Sie den Namen der Schriftart in das **typeface**-Attribut des Schriftartenplatzes ein. Das folgende Beispiel zeigt eine websichere Schriftart, die in einem Schriftartenschema verwendet wird.
  
    
    

```xml

<s:fontSlot name="title">
  <s:latin typeface="Georgia"/>
???
</s:fontSlot>
```


### <a name="web-fonts"></a>Webschriftarten
<a name="webFont"> </a>

Webschriftarten sind Schriftarten, die im Internet verfügbar sind. Wenn ein Benutzer eine Website anzeigt, die Webschriftarten verwendet, lädt der Webbrowser mit der restlichen Seite die erforderlichen Schriftartendateien herunter. Um eine Webschriftart anzugeben, müssen Sie die URL zu Ihren Webschriftartendateien in vier Schriftartenformaten angeben (für browserübergreifende Unterstützung) sowie ein kleines und ein großes Miniaturbild, mit dem die Schriftartennamen in der Schriftartenschemaauswahl wiedergegeben werden.
  
    
    
Das folgende Beispiel beschreibt die Informationen, die erforderlich sind, um eine Webschriftart in einem **<s:latin>**-Element zu verwenden.
  
    
    



```xml

<s:latin typeface="FontName"
  eotsrc="EotFile"
  woffsrc="WoffFile"
  ttfsrc="TtfFile"
  svgsrc="SvgFile"
  largeimgsrc="LargeImgFile"
  smallimgsrc="SmallImgFile" />

```

In diesem Beispiel für die Verwendung einer Webschriftart würden die folgenden Platzhalter ersetzt werden:
  
    
    

-  _FontName_ ist der Name der Webschriftart.
    
  
-  _EotFile_ ist die relative URL zur Embedded OpenType-Schriftartendatei.
    
  
-  _WoffFile_ ist die relative URL zur Web Open Font Format-Schriftartendatei.
    
  
-  _TtfFile_ ist die relative URL zur TrueType-Schriftartendatei.
    
  
-  _SvgFile_ ist die relative URL zur Scalable Vector Graphics-Schriftartendatei.
    
  
-  _LargeImgFile_ ist die relative URL zum großen Miniaturbild, das Sie in der Schriftartenschemaauswahl verwenden möchten.
    
  
-  _SmallImgFile_ ist die relative URL zum kleinen Miniaturbild, das Sie in der Schriftartenschemaauswahl verwenden möchten.
    
  

### <a name="font-slots"></a>Schriftartenplätze
<a name="fontSlot"> </a>

Tabelle 1 beschreibt die verfügbaren Schriftartenplätze und die Stellen, an denen sie in einer Seite verwendet werden.
  
    
    

**Tabelle 1. Schriftartenplätze**


|**Name des Schriftartenplatzes**|**Beschreibung**|
|:-----|:-----|
|title  <br/> |Wird für den Seitentitel verwendet  <br/> |
|Navigation  <br/> |Wird für die horizontalen und vertikalen Navigationselemente auf der Seite verwendet  <br/> |
|large-heading  <br/> |Wird für die H1-Überschrift verwendet  <br/> |
|heading  <br/> |Wird für H2- und H3-Überschriften, Webpart-Titel, Dialogfeldtitel und Popuptitel verwendet  <br/> |
|small-heading  <br/> |Wird für H4-Überschriften verwendet  <br/> |
|large-body  <br/> |Wird für großen Fließtext verwendet (15 Pixel und 19 Pixel)  <br/> |
|body  <br/> |Die Basisschriftart, die an allen anderen Stellen auf der Seite verwendet wird  <br/> |
   

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>


-  [Übersicht über Designs für SharePoint](themes-overview-for-sharepoint.md)
    
  
-  [Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint](how-to-deploy-a-custom-theme-in-sharepoint.md)
    
  
-  [Aktualisieren benutzerdefinierter Designs und CSS-Dateien auf SharePoint](upgrade-custom-themes-and-css-to-sharepoint.md)
    
  
-  [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [SharePoint-Teamblog: Beweisen Sie Stil mit SharePoint-Designs](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  
-  [SharePoint Design Manager - Branding- und Designfunktionen](sharepoint-design-manager-branding-and-design-capabilities.md)
    
  

  
    
    

