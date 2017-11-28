---
title: Verwendung zusammengesetzt sucht nach Marke SharePoint-Websites
ms.date: 11/03/2017
ms.openlocfilehash: ebf4fa0e503cb8c811c6e7ac549d1b89998c1a7d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-composed-looks-to-brand-sharepoint-sites"></a>Verwendung zusammengesetzt sucht nach Marke SharePoint-Websites

Gelten Sie zusammengesetzten, einschließlich Farben, Schriftarten und eines Hintergrundbilds, um Ihre SharePoint 2013 und SharePoint Online-Websites mithilfe von SharePoint Designmodul.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Sie können Ihre SharePoint-Websites zusammengesetzten zuweisen. Zusammengesetzten sind Out-of-Box-Designs, die in SharePoint 2013 und SharePoint Online enthalten sind. Wählen Sie **Websiteeinstellungen**aus, um ein zusammengesetztes Design auf einer SharePoint-Website anzuwenden, > **Aussehen und Verhalten** > **Erscheinungsbild ändern**. Klicken Sie dann können der Änderung der Assistent aussehen zum Anpassen der Farben, Schriftarten, Gestaltungsvorlage und Hintergrundbild des ein zusammengesetztes Design. Die Änderung der Assistent aussehen kopiert, überträgt und CSS, in SharePoints-Inhaltsdatenbank gespeichert. Außerdem recolors Bilder und speichert sie in der Inhaltsdatenbank. 

## <a name="sharepoint-theming-engine"></a>SharePoint-Designmodul
<a name="sectionSection0"> </a>

SharePoint 2013 Designmodul können Farben, Schriftarten und eines Hintergrundbilds zu einer Website durch Zuordnen dieser Elemente zu einer Gestaltungsvorlage anwenden.

In SharePoint 2013 und SharePoint Online ist ein Design ein verbundener XML-Definitionsdateien, einer Bilddatei und eine Masterseite zugeordnet ist, mit denen Sie benutzerdefinierte CSS auf einer Website anwenden. Die folgenden XML-Dateien definieren farbplätze und schriftartenplätze, die die Details zu bestimmten Farben und Schriftarten definieren, wie sie auf Formatvorlagen angewendet werden: 

- .spcolor
    
- .spfont
    
Sie können Ihre eigenen Dateien Farbe und Schriftart in Ihrer bevorzugten Text-Editor erstellen.

In der folgenden Tabelle sind die Elemente des ein zusammengesetztes Design.

|**Element**|**Datei oder Dateien**|**Wo sie gespeichert werden**|**Erforderlich?**|
|:-----|:-----|:-----|:-----|
|Farbpalette|.spcolor|Design Gallery\15 Ordner|Ja|
|Schriftartenschema|.spfont|Design Gallery\15 Ordner|Nein|
|Layout der Website|<p>Master</p><p>.Preview</p>|Gestaltungsvorlagenkatalog|Ja|
|Hintergrundbild|<p>JPG</p><p>BMP</p><p>PNG</p><p>GIF</p>|Website-Objekten|Nein|
Benutzer können mithilfe der Änderung des Assistenten aussehen zusammengesetzten auswählen (**Site Settings** > **Aussehen und Verhalten** > **Erscheinungsbild ändern**), der erste Schritte-Benutzeroberfläche oder direkt in im Menü Websiteaktionen. Wenn ein Benutzer ein zusammengesetztes Design auswählt, wendet Designmodul Farben, Schriftarten, Hintergrundbilder, die zugehörigen Master-Seite und der .preview-Datei, die die master-Seite auf der Website zugeordnet. 

### <a name="color-palettes"></a>Farbpaletten

Designmodul speichert Farben in Farbpaletten, die von der Datei .spcolor definiert, wie in Abbildung 1 dargestellt. Farbpaletten werden in den Designkatalog der Stammwebsite gespeichert. Eine Farbpalette ist eine Farbe Palette Definitionen und Farbe Steckplätze bestehen bearbeitbaren XML-Datei. Farbe der Palette Metadaten ( `<s:colorPalette>`) definiert die folgenden:

- Drei Vorschau anzeigen, die definieren, welche Farbe für die Verwendung in einer Vorschau zusammengesetztes Design Steckplätze Slots.
    
- Eine **IsInverted** -Eigenschaft, mit der der Palette Designer angeben, ob das Design invertiert ist (dunkler Hintergrund mit heller Text).
    
- Der XML-Namespace das Design zugeordnet.
    
Farbplätze definiert zwei Attributesâ€ "Farbe Name und Valueâ€", die einen Namen für die Farbe und RGB-Wert zu definieren. Farbplätze haben semantische Namen wie BodyText oder SiteTitle, die einen Bereich einer SharePoint-Seite Hilfe Sie identifizieren, welche Steckplätze entsprechen.

`<s:color name="BodyText" value="444444" />`

**Abbildung 1. .spcolor-Datei**

![Screenshot einer .spcolor-Datei mit Farbe Name und Value-Attribute](media/16de0716-2e21-471f-b9e5-f461a33b397b.png)

Zeile 2 der Datei .spcolor definiert den XML-Namespace Steckplätze Vorschau, und gibt an, ob die Farben umgekehrt werden (weisen sie einen hellen Vordergrund auf eine dunkler Hintergrund anstelle einer dunkler Vordergrund auf Hintergrund). 

Die .spcolor-Datei enthält 89 farbplätze. Farbplätze können Sie um umfassendere Aspekte der Farbe, einschließlich Durchlässigkeit, mithilfe von Hexadezimalwerte 8 Ziffern zu definieren. Beispielsweise grün ist RRGGBB 00FF00 ein 70 Prozent undurchsichtig grüner AARRGGBB 7F00FF00 ist. Wenn SharePoint einen Steckplatz, den Sie definieren verwendet, werden keine CSS, die darauf verweist Farbe zu ändern. Wenn ein Steckplatz definiert ist, die nie in CSS verwiesen wird, wird die Farbe nie in der Benutzeroberfläche angezeigt.

Sie können die .spcolor-Datei in Editor bearbeiten. Es kann in PowerPoint nicht bearbeitet werden.

### <a name="color-palette-tool"></a>Farbe Palette tool

Die [Farbe Palette Tool](http://www.microsoft.com/en-us/download/details.aspx?id=38182) können zum Visualisieren Designfarben und wie sie auf der Seite zusammenarbeiten. Verwenden Sie es zum Identifizieren der Farbinformationen können Sie in der farbplätze der Datei .spcolor verwenden und Farben auf einer SharePoint-Website anwenden, ohne alle CSS im Rahmen des Prozesses ändern.

Das Tool zeigt die Farben im Hexadezimal-Format, sodass Sie können auf einfache Weise kopieren und fügen den Color-Wert in das entsprechende Element in der Datei .spcolor. Das Tool Farbe Palette können auch ein Hintergrundbild in einem Modell und Umschalten zwischen der Gestaltungsvorlagen seattle.master und oslo.master passen. 


**Abbildung 2. Farbe Palette tool**

![Screenshot des Tools Palette Farbe](media/407d8095-20cd-4d9b-be53-493d95b4653c.png)

Die Datei .spcolor ist die einzige Datei, die für ein neues Design erforderlich ist, jedoch müssen Sie möglicherweise einige benutzerdefinierte Schriftart Deklarationen, je nach die Extrusionstiefe der Entwurfszeit hinzufügen. Dazu müssen Sie die .spfont-Datei zugreifen.

### <a name="font-schemes"></a>Schriftartenschemas

Auf die gleiche Weise, dass Farbpaletten definieren, wie die Farben in zusammengesetzten verwendet werden definieren Schriftartenschemas Schriftarten in der zusammengesetzten. 

Schriftartenschemas sind in der .spfont-Datei in den Designkatalog gespeicherten definiert. Die .spfont-Datei umfasst die folgenden schriftartenplätze, die den Namen, Schriftart und Skript Werte ein zusammengesetztes Design zu definieren:

- Titel
    
- Navigation
    
- Kleine-Überschrift
    
- Überschrift
    
- Large-Überschrift
    
- Body
    
- Großer Textkörper
    
Schriftarten sind weitere von Skripttyp (z. B. Lateinisch, Arabisch, Kyrillisch) beschränkt. Unterstützung für Web Schriftarten ist in vier Dateitypen enthalten:

- Eingebettete open Typ EOT)
    
- Web open Font Format-Datei (WOFF)
    
- TrueType-Schriftart (TTF)
    
- Skalierbare Vektorgrafiken (SVG)
    
Das Schriftartenschema definiert einen großen Vorschaubild und eine kleine Vorschaubild. Sie sind nur für Webschriftarten erforderlich.

**Hinweis**  Sie können die .spfont-Datei in Editor bearbeiten. Es kann in PowerPoint nicht bearbeitet werden.

Es folgt ein Beispiel einer .spfont-Datei.

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

### <a name="site-layout-master-pages-and-corresponding-preview-files"></a>Layout der Website: Masterseiten und entsprechende Vorschaudateien

Designmodul definiert das Layout Website einen durchkomponierten Look basierend auf der Masterseite Master und die entsprechenden .preview-Datei. Wenn die Masterseite für die zusammengesetztes Design definierten seattle.master ist, definiert die Masterseite beispielsweise das Layout der Website.

Das Layout der Website entnommen the Master Page Gallery von Masterseiten, die begleitenden .preview Dateien vorhanden sind. Eine Datei .preview ist erforderlich für eine Gestaltungsvorlage als Option für die **Änderung des Erscheinungsbilds** Benutzeroberfläche angezeigt werden (**Websiteeinstellungen** > **Aussehen und Verhalten** > **Erscheinungsbild ändern**).

Erstellen Sie eine Gestaltungsvorlage im Dropdown-Menü Layout der Website zur Verfügung zu stellen, eine .preview-Datei, die die master-Seite entspricht. Die Datei .preview Zeigt Miniaturansichten für zusammengesetztes Design und im Vorschaubereich rechts neben der Optionen auf der Seite designbuilder.aspx **Erscheinungsbild ändern** .

### <a name="background-image"></a>Hintergrundbild

Sie können das Hintergrundbild des ein zusammengesetztes Design ändern, indem Sie auf **Ändern**. Daraufhin wird ein Dialogfeld hochladen, die Sie zum Hochladen einer Bilddatei verwenden können. Sie können auch Ihr eigenes Bild auf den Hintergrund Preview ziehen.

## <a name="create-custom-themes"></a>Erstellen benutzerdefinierter Designs
<a name="sectionSection1"> </a>

So erstellen Sie ein benutzerdefiniertes Design:

1. Wechseln Sie auf **websiteeinstellungen**, und klicken Sie unter der Überschrift Web-Designer-Kataloge, wählen Sie **Designs** > **15**. Eine Liste der .spcolor und .spfont-Dateien wird angezeigt, wie in Abbildung 3 dargestellt.
    
    **Abbildung 3. Designkatalog**

    ![Screenshot von den Designkatalog, der zeigt Fontscheme und Pallette-Dateien](media/76e9b4f3-5838-4cd8-9f2f-33a0c94bfddd.png)

2. Laden Sie eine Kopie einer der .spcolor-Dateien (beispielsweise Palette001.spcolor), und öffnen Sie es in einem Text-Editor. 
    
3. Bearbeiten der Datei kopierten .spcolor entsprechend Ihrer Entwurfsrichtlinien. Angenommen, wenn Sie eine schwarze Schriftart für Textkörper haben, bearbeiten Sie die Datei zur Änderung der Linie `<s:color name="BodyText" value="444444" />` auf `<s:color name="BodyText" value="000000" />`.
    
4. Fügen Sie für jedes HTML-Element eine Farbe hinzu. 
    
5. Wenn Sie fertig sind, laden Sie die .spcolor-Datei mit den **websiteeinstellungen** > **Design** > **15** Ordner.
    
    **Hinweis**  Speichern Sie die Datei unter einem neuen Namen (beispielsweise custom_palette1.spcolor).

   In der folgenden Tabelle ordnet Farben und Seitenelemente ihr Code in der Datei .spcolor. Es ist eine Teilmenge der Zuordnungen, die in der Datei .spcolor verfügbar sind.
    

    |**Element**|**Farbe**|**Code**|
    |:-----|:-----|:-----|
    |Textkörper|Schwarz| `<s:color name="BodyText" value="000000" />`|
    |Globale Navigation Hintergrund|Blau| `<s:color name="HeaderBackground" value="018dff" />`|
    |Text für die globale navigation|Whitepaper| `<s:color name="HeaderNavigationText" value="ffffff" />`|
    |Aktuelle Navigation Hintergrund|Rot| `<s:color name="NavigationHoverBackground" value="e51400" />`|
    |Text für die aktuelle navigation|Whitepaper| `<s:color name="Navigation" value="ffffff" />`|
    |Titel|Whitepaper| `<s:color name="SiteTitle" value="FFFFFF" />`|
    |Fußzeile Hintergrund|Schwarz| `<s:color name="FooterBackground" value="000000" />`|

6. Informationen zum Anpassen von .spfont Herunterladen einer Kopie einer .spfont-Datei, und öffnen Sie es in einem Text-Editor. Beachten Sie, dass die .spfont-Datei ein wenig anders als .spcolor angeordnet ist, aber beide Dateien eine ähnliche Struktur freigeben. 
    
    **Abbildung 4. .spfont-Datei**

    ![Screenshot, der den Inhalt der .spfont-Datei anzeigt](media/893f905a-34d9-4dbd-a012-03797084f9e6.png)

7. Bearbeiten Sie jede `<s:fontSlot />` Abschnitt zum Anpassen der Schriftart SharePoint gilt für die angegebene Schriftart Steckplatz auf der Seite. Beachten Sie beispielsweise den ersten Eintrag, `<s:fontSlot name="title">`. Dieser Eintrag wird beschrieben, welche Schriftart SharePoint verwendet, um den Titel der Seite zu formatieren. In diesem Abschnitt gibt auch an, welche Schriftart für verschiedene Sprachen verwendet werden soll.
    
    **Hinweis**  Sie können hochladen benutzerdefinierte Schriftarten in SharePoint und zeigen Sie jeden Eintrag auf eine benutzerdefinierte .eot, .woff, ttf und SVG-Datei. 

8. Laden Sie die Datei mit den **websiteeinstellungen** > **Design** > **15** Ordner.
    
    **Hinweis**  Speichern Sie die Datei unter einem neuen Namen (beispielsweise custom_font.spfont).

    In der folgenden Tabelle ordnet Schriftarten Seitenelemente wie sie in der .spfont-Datei definiert sind.

|**Element**|**Schriftart**|**Code**|
|:-----|:-----|:-----|
|Titel|Sans öffnen| `<s:cs typeface="Open Sans" />`|
|Navigation|Roboto| `<s:cs typeface="Roboto" />`|
|Überschriften|Trajan Pro| `<s:cs typeface="Trajan Pro" />`|
|Body|Sans öffnen| `<s:cs typeface="Open Sans" />`|

Möglicherweise müssen Sie sicherstellen, dass einige benutzerdefinierten Schriftarten Browser Benutzer zur Verfügung stehen. Bezieht sich die Überschriften auf eine Trajan Pro Schriftart, die auf die meisten Benutzercomputern ungewöhnlich ist, fügen Sie die folgenden Deklarationen von Schriftart am oberen Rand der Deklaration < S:fontSlot > fest. Dadurch wird sichergestellt, dass die richtige Schriftart angezeigt wird. 

```XML
<s:latin typeface=" Trajan Pro" eotsrc="/SiteAssets/Trajan Pro.eot" woffsrc="/SiteAssets/Trajan Pro.woff" ttfsrc="/SiteAssets/Trajan Pro.ttf" svgsrc="/SiteAssets/Trajan Pro.svg"  />
```

## <a name="add-a-custom-theme-to-sharepoint"></a>Hinzufügen eines benutzerdefinierten Designs in SharePoint
<a name="sectionSection2"> </a>

Nachdem Sie Ihre Anpassungen an der Gestaltungsvorlage, .spcolor und .spfont-Dateien vornehmen, fügen sie in das Verzeichnis zusammengesetzten hinzu, damit SharePoint, darauf zugreifen kann. 

1. Wechseln Sie auf **websiteeinstellungen**, und klicken Sie unter **Web-Designer-Kataloge**, und wählen Sie **Zusammengesetzten**. 
    
2. Wählen Sie den Link **Neues Element** oben links aus. Ein Fenster geöffnet wird, wie in Abbildung 5 dargestellt.
    
    **Abbildung 5. Zusammengesetzten**

    ![Screenshot, der auf der Seite neue zusammengesetztes Design wird](media/8155ba5d-9492-473d-b153-c3db566cbdec.png)

3. Fügen Sie einen Titel und einen Namen für Ihre zusammengesetztes Design.
    
4. Führen Sie das verbleibende dar:
    
    - Fügen Sie im Feld **Master-Seiten-URL** die URL der Masterseite, die Sie Designs verwenden möchten.
    
    - Fügen Sie im Feld **Design-URL** die URL der Datei .spcolor hinzu.
    
    - Schließen Sie im Feld **Bild-URL** die URL eines Bilds, das Sie als Hintergrund verwenden möchten. Dies ist nicht erforderlich, wenn Ihre Umgebung für ein Hintergrundbild Aufrufen nicht.
    
    - Schließen Sie in das Feld **Schriftart Schema URL** die URL der .spfont-Datei.
    
    - Geben Sie im Feld **Anzeigereihenfolge** an, die Reihenfolge, in der zusammengesetzte Design angezeigt werden soll.
    
5. Wählen Sie **Speichern** aus. Ihre Eingabe Design wird nun in der Liste **Durchkomponierte** angezeigt werden.
    
Nach dem Hinzufügen Ihrer benutzerdefinierten Designs aus, um als ein zusammengesetztes Design Benutzer das Design zugreifen und es zu einer Website anwenden, indem Sie auf **websiteeinstellungen** > **Aussehen und Verhalten** > **Erscheinungsbild ändern**. Abbildung 6 zeigt ein Beispiel eines Abschnitts **Erscheinungsbild ändern** , in den **Websiteeinstellungen**.

**Abbildung 6. Zusammengesetzten in Erscheinungsbild ändern verfügbar**

![Screenshot, der anzeigt, die zusammengesetzten sucht, stehen in den Websiteeinstellungen > Ändern der Darstellung](media/11acb4ea-cff6-483c-890f-8c574e14f29d.png)

## <a name="what-does-the-theming-engine-do-when-a-user-applies-a-composed-look"></a>Was geschieht Designmodul? Wenn ein Benutzer ein zusammengesetztes Design angewendet wird.
<a name="sectionSection3"> </a>

Wenn ein Benutzer ein zusammengesetztes Design angewendet wird, wird SharePoint kopiert, überträgt und speichert in der Inhaltsdatenbank CSS. Außerdem recolors und speichert Bilder in der Inhaltsdatenbank. Im Rahmen des Prozesses zum Anwenden eines Designs auf eine Website zieht Designmodul Farbe und Schriftart Werte aus der angegebenen Farbe Farbpalette und ein Schriftartenschema in den Designkatalog der Stammwebsite gefunden wurde. Zum Anwenden von Master-Seite und die .preview Gestaltungsvorlagendatei (das Layout der Website) zieht Designmodul Gestaltungsvorlagen in the Master Page Gallery, die eine entsprechende Datei .preview aufweisen. 

Wenn sie ein zusammengesetztes Design angewendet wird, ordnet das Modul die Einstellungen, die durch bestimmte CSS-Kommentare, die Designmodul definiert angegeben. Designmodul im Detail speichert das Hintergrundbild auf Website-Objekten, skalierbar und JPG und BMP Bilder komprimiert und beschränkt die Größe von GIF und PNG-Bilder. 

Wenn ein zusammengesetztes Design auf einer SharePoint-Website angewendet wird, SharePoint sucht und CSS-Kommentartoken durch Einbetten eines Werts, der die zusammengesetztes Design in die nächste Zeile in der CSS-Datei nach dem Token abgeleiteten ersetzt. In diesem neue Wert wird auf der SharePoint-Website angewendet.

Die folgende Tabelle enthält die CSS-Kommentar-Token.

|**Token**|**Beschreibung**|**Entsprechende ApplyTheme-parameter**|
|:-----|:-----|:-----|
|/ * ReplaceBGImage * /|Aktuelle Hintergrundbild mit dem Bild in der zugewiesenen vertauscht zusammengesetzt aussehen Bild-URL.|backgroundImageUrl|
|/ * ReplaceFont * /|Wechselt von der aktuellen Schriftart mit einem der Schriftarten, die in der Schriftart Schema URL von der zugewiesenen zusammengesetztes Design gefunden.|fontSchemeUrl|
|/ * ReplaceColor * /|Vertauscht die aktuelle Farbe mit einem der in einer farbplatzes in der Farbe Palette URL von der zugewiesenen zusammengesetztes Design angegebenen Farben.|colorPaletteUrl|
|/ * RecolorImage * /|Recolors Bilder mit Farbton anpassen oder ausfüllen. ||

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Lösungen für das SharePoint-Websitebranding und die Seitenanpassung](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website](Branding-and-site-provisioning-solutions-for-SharePoint.md)
