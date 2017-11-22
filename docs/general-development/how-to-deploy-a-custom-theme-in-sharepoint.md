---
title: Vorgehensweise Bereitstellen eines benutzerdefinierten Designs in SharePoint
ms.date: 09/25/2017
ms.prod: sharepoint
ms.assetid: f703df24-8e56-4e6a-bc37-95acbb3c83e8
ms.openlocfilehash: 002ee3e01c3d68f28ceb4ac3e8c9f66b4a1dec8c
ms.sourcegitcommit: 11d9185437fc819ab41421c0f4fe06aa300b9d28
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/25/2017
---
# <a name="how-to-deploy-a-custom-theme-in-sharepoint"></a>Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint
Hier finden Sie Informationen dazu, wie Sie mithilfe der Benutzeroberfläche oder durch Implementierung eines Featureempfängers ein benutzerdefiniertes Design auf einer SharePoint-Website bereitstellen. SharePoint enthält vorinstallierte Designs. Sie können zusätzliche Farbpaletten, Schriftartenschemas und Gestaltungsvorlagen erstellen und so benutzerdefinierte Designs erstellen. Sobald die Dateien in die Design Gallery und den Gestaltungsvorlagenkatalog hochgeladen wurden, können Sie ein Design mithilfe der Benutzeroberfläche oder mithilfe von Code bereitstellen. Weitere Informationen zu Farbpaletten und Schriftartenschemas finden Sie unter  [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).
  
    
> [!NOTE]
> Dieser Artikel gilt nur für klassische SharePoint-Websiteoberflächen. Detaillierte Informationen zu modernen SharePoint-Websites und deren Unterstützung für Designs finden Sie im Artikel [SharePoint-Websitedesign](https://docs.microsoft.com/de-DE/sharepoint/dev/declarative-customization/site-theming/sharepoint-site-theming-overview).


## <a name="core-concepts-to-know-to-deploy-a-theme"></a>Die wichtigsten Konzepte für die Bereitstellung eines Designs
<a name="core"> </a>

In Tabelle 1 sind Artikel aufgeführt, die grundlegende Informationen zu den Kernkonzepten der Bereitstellung von Designs enthalten.
  
    
    

**Tabelle 1. Kernkonzepte zur Bereitstellung eines Designs**


|**Titel des Artikels**|**Beschreibung**|
|:-----|:-----|
| [Übersicht über Designs für SharePoint](themes-overview-for-sharepoint.md) <br/> |Informationen zur Designoberfläche in SharePoint.  <br/> |
| [Featureereignisse](http://msdn.microsoft.com/de-DE/library/ms469501.aspx) <br/> |Informationen zu Featureereignissen, die es Ihnen ermöglichen, ein Ereignis abzufangen und darauf zu reagieren, wenn ein Feature in der Serverfarm installiert ist.  <br/> |
   

## <a name="upload-files-to-the-theme-gallery-and-the-master-page-gallery"></a>Hochladen von Dateien in die Design Gallery und den Gestaltungsvorlagenkatalog
<a name="section1"> </a>

Sie können benutzerdefinierte Designs erstellen, indem Sie zusätzliche Farbpaletten und Schriftartenschemas erstellen und diese in die Design Gallery hochladen. Die neuen Farbpaletten und Schriftartenschemas stehen Ihnen dann zur Verfügung, wenn Sie ein Design in der Designoberfläche ändern, oder wenn Sie ein Design programmgesteuert anwenden. Genauso können Sie zusätzliche Gestaltungsvorlagen und entsprechende Vorschaudateien in den Gestaltungsvorlagenkatalog hochladen, wenn Sie zusätzliche Websitelayouts zur Auswahl haben möchten. In der folgenden Liste wird beschrieben, wo Sie die Dateien ablegen.
  
    
    

- **Gestaltungsvorlagenkatalog** Führt die Gestaltungsvorlagendateien und die entsprechenden Vorschaudateien (.preview-Dateien) auf. Sie benötigen eine Vorschaudatei für Gestaltungsvorlagen, wenn die Gestaltungsvorlage im Assistent **Aussehen ändern** verfügbar sein soll. JavaScript-Dateien und andere Designressourcen können auch in den Gestaltungsvorlagenkatalog hochgeladen werden.
    
    Um den Gestaltungsvorlagenkatalog über die Benutzeroberfläche von SharePoint aufzurufen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** **Gestaltungsvorlagen** aus. Sie können auch direkt zu der Website navigieren (http:// _SiteName_/_catalogs/masterpage/).
    
  
- **Design Gallery** Führt die Farbpaletten und Schriftartenschemas auf, die in der Designoberfläche verfügbar sind. SharePoint sucht im Ordner **15**, um die verfügbaren Farbpaletten und Schriftartenschemas zu ermitteln.
    
    Um die Design Gallery über die Benutzeroberfläche von SharePoint aufzurufen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** **Designs** aus. Sie können auch direkt zu der Website navigieren (http:// _SiteCollectionName_/_catalogs/theme/15).
    
  
- **Formatbibliothek** Führt die benutzerdefinierten CSS-Dateien auf, die Sie in der Designoberfläche verwenden möchten. Sie können direkt zur Formatbibliothek navigieren (ersetzen Sie _SiteCollectionName_ und _language_ in dieser URL: http:// _SiteCollectionName_/Style Library/ _language_/Themable/).
    
    > **Hinweis:** Legen Sie die benutzerdefinierten CSS-Dateien im Ordner „Themable“ in der Formatvorlagenbibliothek ab, nicht im Ordner „Themable“ im Gestaltungsvorlagenkatalog. Das Designmodul erkennt ausschließlich die CSS-Dateien im Ordner „Themable“ in der Formatvorlagenbibliothek. 

> **Hinweis:** Wenn Sie im Gestaltungsvorlagenkatalog und im Designkatalog die Versionsverwaltung aktiviert haben, müssen Sie die Designdateien außerdem zuerst veröffentlichen, damit das Designmodul sie verwenden kann. 
  
    
    


## <a name="deploy-a-theme-by-using-the-user-interface"></a>Bereitstellen eines Designs mithilfe der Benutzeroberfläche
<a name="section2"> </a>

Unter einem durchkomponierten Look oder einem Design versteht man die Farbpalette, das Schriftartenschema, das Hintergrundbild und die Gestaltungsvorlage, welche das Erscheinungsbild einer Website bestimmen. Die Liste "Durchkomponierte Looks" enthält die durchkomponierten Looks, die in der Design Gallery verfügbar sind. Sie können ein Design erstellen, indem Sie in der Liste "Durchkomponierte Looks" ein Listenelement hinzufügen und angeben, welche Gestaltungsvorlage, welche Farbpalette, welches Schriftartenschema und welches Hintergrundbild verwendet werden soll.
  
    
    

> **Hinweis:** Soll die Gestaltungsvorlage im Designkatalog verfügbar sein, benötigen Sie für die Gestaltungsvorlage eine Vorschaudatei. 
  
    
    


### <a name="to-add-a-composed-look"></a>Hinzufügen eines durchkomponierten Looks


1. Wählen Sie das Symbol **Einstellungen** und dann **Websiteeinstellungen** aus.
    
  
2. Wählen Sie unter **Web-Designer-Kataloge** **Durchkomponierte Looks** aus.
    
  
3. Wählen Sie in der Liste **Durchkomponierte Looks** **Neues Element** aus.
    
  
4. Geben Sie im Textfeld **Titel** einen Titel für das Design ein.
    
  
5. Geben Sie im Textfeld **Name** einen Namen für das Design ein. Der Name wird in der Liste "Durchkomponierte Looks" und in der Design Gallery angezeigt.
    
  
6. Geben Sie im Textfeld ** Gestaltungsvorlagen-URL** die URL der Gestaltungsvorlage ein. Die URL kann eine relative URL sein.
    
  
7. Geben Sie im Textfeld **Design-URL** die URL der Farbpalette (die URL zur .spcolor-Datei) ein. Die URL kann eine relative URL sein.
    
  
8. Geben Sie im Textfeld **Bild-URL** die URL zum Hintergrundbild ein. Dies ist optional. Die URL kann eine relative URL sein.
    
  
9. Geben Sie im Textfeld **Schriftartenschema-URL** die URL des Schriftartenschemas (die URL zur .spfont-Datei) ein. Dies ist optional. Die URL kann eine relative URL sein.
    
  
10. Geben Sie im Textfeld **Anzeigereihenfolge** die Nummer der Anzeigereihenfolge ein. Hiervon hängt ab, wo das Design in der Design Gallery angezeigt wird.
    
  
11. Klicken Sie auf **Speichern**.
    
    > **Hinweis:** Sind die Werte des durchkomponierten Looks fehlerhaft, wird der durchkomponierte Look nicht zum Designkatalog hinzugefügt. In einem solchen Fall wird keine Meldung in die Protokolldateien geschrieben. Wenn ein durchkomponierter Look nicht hinzugefügt werden kann, kann das folgende Gründe haben: Eine Datei wurde nicht gefunden, in einer der Dateien gibt es Formatierungsfehler, oder SharePoint kann nicht auf die Dateien zugreifen. 
      > Nun können Sie das neue Design über den Designkatalog auf Ihre Website anwenden. Weitere Informationen finden Sie unter [Auswählen eines Designs für Ihre Veröffentlichungswebsite](http://office.microsoft.com/de-DE/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx) auf Office.com.
  
    
    

## <a name="deploy-a-theme-by-using-code"></a>Bereitstellen eines Designs mithilfe von Code
<a name="section3"> </a>

Sie können ein Design durch die Implementierung eines Featureempfängers bereitstellen.
  
    
    

### <a name="to-deploy-a-theme-by-using-a-feature-receiver"></a>So stellen Sie ein Design mithilfe eines Featureempfängers bereit


1. Erstellen Sie eine Featureempfängerklasse, die von der  [SPFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.aspx) -Klasse erbt.
    
  
2. Erstellen Sie in der  [FeatureActivated](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.FeatureActivated.aspx) -Methode ein [SPTheme](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPTheme.aspx) -Objekt, das die Farbpalette und das Schriftartenschema verwendet, und wenden Sie das Design dann auf Ihre Website an.
    
    Das folgende Codebeispiel demonstriert, wie Sie eine benutzerdefinierte Farbpalette und ein benutzerdefiniertes Schriftartenschema auf eine Website anwenden können:
    


```cs
  
// Get the SPColor file. Replace with the path to your SPColor file.
SPFile colorPaletteFile = Web.GetFile("path to .spcolor file");
if (null == colorPaletteFile || !colorPaletteFile.Exists)
{
    // TODO: handle the error.
    return;
}

// Get the SPFont file. Replace with the path to your SPFont file.
SPFile fontSchemeFile = Web.GetFile("path to .spfont file");
if (null == fontSchemeFile || !fontSchemeFile.Exists)
{
    // TODO: handle the error.
    return;
}

// Open an SPTheme with the two files. Replace NewTheme with the name for your theme.
// Note: If you have a background image, you can specify the following:
// SPTheme.Open("NewTheme", colorPaletteFile, fontSchemeFile, backgroundURI)
SPTheme theme = SPTheme.Open("NewTheme", colorPaletteFile, fontSchemeFile);


// Now apply your theme to the site.
// The themed CSS output files are stored in the Themed folder of the Theme Gallery of the root web
// of the site collection. To specify that the files should be stored in the _themes folder within the root 
// web, pass false to the ApplyTo method.
theme.ApplyTo(Web, true);
```


    > **Note:**
      > The  _shareGenerated_ parameter in the **ApplyTo** method specifies whether the themed files can be shared across sites in a site collection. In general, it is set to **true** for SharePoint Server and SharePoint Online sites and set to **false** for SharePoint Foundation sites. The _shareGenerated_ parameter must be set to **true** if you intend the themed files to be shared. For more information, see [ApplyTo(SPWeb, Boolean)](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPTheme.ApplyTo.aspx) .

    When a user applies a theme in the **Change the look** wizard, the wizard also updates a theme named Current in the Composed Looks list and the design gallery. When you apply a theme programmatically, you have to update the Current theme manually. The following example shows how to update the Current theme.
    


```cs
  
SPList designGallery = Web.GetCatalog(SPListTemplateType.DesignCatalog);
if (null == designGallery)
{
    // TODO: Handle the error.
    return;
}

SPQuery q = new SPQuery();
q.RowLimit = 1;
q.Query = "<Where><Eq><FieldRef Name='DisplayOrder'/><Value Type='Number'>0</Value></Eq></Where>";
q.ViewFields = "<FieldRef Name='DisplayOrder'/>";
q.ViewFieldsOnly = true;

SPListItemCollection currentItems = designGallery.GetItems(q);

If (currentItems.Count == 1)
{
    // Remove the old Current item.
    currentItems[0].Delete();
}

SPListItem currentItem = designGallery.AddItem();

currentItem["Name"] = SPResource.GetString(CultureInfo.CurrentUICulture, Strings.DesignGalleryCurrentItemName);
currentItem["Title"] = SPResource.GetString(CultureInfo.CurrentUICulture, Strings.DesignGalleryCurrentItemName);

// Change this line if you want to specify a different master page.
currentItem["MasterPageUrl"] = Web.MasterUrl;

// Replace with the path to your SPColor file.
currentItem["ThemeUrl"] = "path to .spcolor file";

// Delete the following line if you do not have a background image. Otherwise, replace with the path to
// the background image.
currentItem["ImageUrl"] = "path to background image"; 

// Replace with the path to your SPFont file. Or, you can delete this line if you want to use
// the default font scheme of the selected master page.
currentItem["FontSchemeUrl"] = "path to .spfont file"; 

currentItem["DisplayOrder"] = 0;
currentItem.Update();

```


## <a name="additional-resources"></a>Weitere Ressourcen
<a name="bk_addresources"> </a>


-  [Entwickeln des Website-Designs in SharePoint](develop-the-site-design-in-sharepoint.md)
    
  
-  [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [SharePoint-Teamblog: Beweisen Sie Stil mit SharePoint-Designs](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  

