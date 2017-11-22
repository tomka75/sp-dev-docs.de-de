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
# <a name="how-to-deploy-a-custom-theme-in-sharepoint"></a><span data-ttu-id="24390-102">Vorgehensweise: Bereitstellen eines benutzerdefinierten Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24390-102">How to: Deploy a custom theme in SharePoint</span></span>
<span data-ttu-id="24390-p101">Hier finden Sie Informationen dazu, wie Sie mithilfe der Benutzeroberfläche oder durch Implementierung eines Featureempfängers ein benutzerdefiniertes Design auf einer SharePoint-Website bereitstellen. SharePoint enthält vorinstallierte Designs. Sie können zusätzliche Farbpaletten, Schriftartenschemas und Gestaltungsvorlagen erstellen und so benutzerdefinierte Designs erstellen. Sobald die Dateien in die Design Gallery und den Gestaltungsvorlagenkatalog hochgeladen wurden, können Sie ein Design mithilfe der Benutzeroberfläche oder mithilfe von Code bereitstellen. Weitere Informationen zu Farbpaletten und Schriftartenschemas finden Sie unter  [Farbpaletten und Schriftarten in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span><span class="sxs-lookup"><span data-stu-id="24390-p101">Learn how to deploy a custom theme to a SharePoint site by using the user interface or by implementing a feature receiver. SharePoint includes preinstalled themes. You can create custom themes by creating additional color palettes, font schemes, and master pages. After the files are uploaded to the Theme Gallery and the Master Page Gallery, you can deploy a theme to a site by using the user interface or by using code. For more information about color palettes and font schemes, see  [Color palettes and fonts in SharePoint](color-palettes-and-fonts-in-sharepoint.md).</span></span>
  
    
> [!NOTE]
> <span data-ttu-id="24390-108">Dieser Artikel gilt nur für klassische SharePoint-Websiteoberflächen.</span><span class="sxs-lookup"><span data-stu-id="24390-108">This article only applies in the context of classic SharePoint site experience.</span></span> <span data-ttu-id="24390-109">Detaillierte Informationen zu modernen SharePoint-Websites und deren Unterstützung für Designs finden Sie im Artikel [SharePoint-Websitedesign](https://docs.microsoft.com/de-DE/sharepoint/dev/declarative-customization/site-theming/sharepoint-site-theming-overview).</span><span class="sxs-lookup"><span data-stu-id="24390-109">If you are looking details around modern SharePoint sites and their theme support, please have a look on the following article - [SharePoint site theming](https://docs.microsoft.com/de-DE/sharepoint/dev/declarative-customization/site-theming/sharepoint-site-theming-overview)</span></span>


## <a name="core-concepts-to-know-to-deploy-a-theme"></a><span data-ttu-id="24390-110">Die wichtigsten Konzepte für die Bereitstellung eines Designs</span><span class="sxs-lookup"><span data-stu-id="24390-110">Core concepts to know to deploy a theme</span></span>
<span data-ttu-id="24390-111"><a name="core"> </a></span><span class="sxs-lookup"><span data-stu-id="24390-111"></span></span>

<span data-ttu-id="24390-112">In Tabelle 1 sind Artikel aufgeführt, die grundlegende Informationen zu den Kernkonzepten der Bereitstellung von Designs enthalten.</span><span class="sxs-lookup"><span data-stu-id="24390-112">Table 1 lists articles that can help you understand the core concepts of deploying themes.</span></span>
  
    
    

<span data-ttu-id="24390-113">**Tabelle 1. Kernkonzepte zur Bereitstellung eines Designs**</span><span class="sxs-lookup"><span data-stu-id="24390-113">**Table 1. Core concepts to deploy a theme**</span></span>


|<span data-ttu-id="24390-114">**Titel des Artikels**</span><span class="sxs-lookup"><span data-stu-id="24390-114">**Article title**</span></span>|<span data-ttu-id="24390-115">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="24390-115">**Description**</span></span>|
|:-----|:-----|
| [<span data-ttu-id="24390-116">Übersicht über Designs für SharePoint</span><span class="sxs-lookup"><span data-stu-id="24390-116">Themes overview for SharePoint</span></span>](themes-overview-for-sharepoint.md) <br/> |<span data-ttu-id="24390-117">Informationen zur Designoberfläche in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="24390-117">Learn about the theming experience in SharePoint.</span></span>  <br/> |
| [<span data-ttu-id="24390-118">Featureereignisse</span><span class="sxs-lookup"><span data-stu-id="24390-118">Feature Events</span></span>](http://msdn.microsoft.com/de-DE/library/ms469501.aspx) <br/> |<span data-ttu-id="24390-119">Informationen zu Featureereignissen, die es Ihnen ermöglichen, ein Ereignis abzufangen und darauf zu reagieren, wenn ein Feature in der Serverfarm installiert ist.</span><span class="sxs-lookup"><span data-stu-id="24390-119">Learn about feature events, which enable you to trap and respond to an event that occurs when a feature is installed in the server farm.</span></span>  <br/> |
   

## <a name="upload-files-to-the-theme-gallery-and-the-master-page-gallery"></a><span data-ttu-id="24390-120">Hochladen von Dateien in die Design Gallery und den Gestaltungsvorlagenkatalog</span><span class="sxs-lookup"><span data-stu-id="24390-120">Upload files to the Theme Gallery and the Master Page Gallery</span></span>
<span data-ttu-id="24390-121"><a name="section1"> </a></span><span class="sxs-lookup"><span data-stu-id="24390-121"></span></span>

<span data-ttu-id="24390-p103">Sie können benutzerdefinierte Designs erstellen, indem Sie zusätzliche Farbpaletten und Schriftartenschemas erstellen und diese in die Design Gallery hochladen. Die neuen Farbpaletten und Schriftartenschemas stehen Ihnen dann zur Verfügung, wenn Sie ein Design in der Designoberfläche ändern, oder wenn Sie ein Design programmgesteuert anwenden. Genauso können Sie zusätzliche Gestaltungsvorlagen und entsprechende Vorschaudateien in den Gestaltungsvorlagenkatalog hochladen, wenn Sie zusätzliche Websitelayouts zur Auswahl haben möchten. In der folgenden Liste wird beschrieben, wo Sie die Dateien ablegen.</span><span class="sxs-lookup"><span data-stu-id="24390-p103">You can create custom themes by creating additional color palettes and font schemes and uploading them to the Theme Gallery. The new color palettes and font schemes are then available to you when you modify a design in the theming experience or when you apply a theme programmatically. Similarly, if you want to have additional site layouts to choose from, you can upload additional master pages, and corresponding preview files, to the Master Page Gallery. The following list describes where to place the files:</span></span>
  
    
    

- <span data-ttu-id="24390-p104">**Gestaltungsvorlagenkatalog** Führt die Gestaltungsvorlagendateien und die entsprechenden Vorschaudateien (.preview-Dateien) auf. Sie benötigen eine Vorschaudatei für Gestaltungsvorlagen, wenn die Gestaltungsvorlage im Assistent **Aussehen ändern** verfügbar sein soll. JavaScript-Dateien und andere Designressourcen können auch in den Gestaltungsvorlagenkatalog hochgeladen werden.</span><span class="sxs-lookup"><span data-stu-id="24390-p104">**Master Page Gallery** Lists the master page files, and their corresponding preview files (.preview files). A master page preview file is required if you want the master page to be available in the **Change the look** wizard. JavaScript files and other design assets can also be uploaded to the Master Page Gallery.</span></span>
    
    <span data-ttu-id="24390-p105">Um den Gestaltungsvorlagenkatalog über die Benutzeroberfläche von SharePoint aufzurufen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** **Gestaltungsvorlagen** aus. Sie können auch direkt zu der Website navigieren (http:// _SiteName_/_catalogs/masterpage/).</span><span class="sxs-lookup"><span data-stu-id="24390-p105">To access the Master Page Gallery from the SharePoint user interface, on the **Site Settings** page, under **Web Designer Galleries**, choose **Master pages**. You can also navigate directly to the site (http://  _SiteName_/_catalogs/masterpage/).</span></span>
    
  
- <span data-ttu-id="24390-p106">**Design Gallery** Führt die Farbpaletten und Schriftartenschemas auf, die in der Designoberfläche verfügbar sind. SharePoint sucht im Ordner **15**, um die verfügbaren Farbpaletten und Schriftartenschemas zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="24390-p106">**Theme Gallery** Lists the color palettes and font schemes that are available to the theming experience. SharePoint looks in the **15** folder to determine the available color palettes and font schemes.</span></span>
    
    <span data-ttu-id="24390-p107">Um die Design Gallery über die Benutzeroberfläche von SharePoint aufzurufen, wählen Sie auf der Seite **Websiteeinstellungen** unter **Web-Designer-Kataloge** **Designs** aus. Sie können auch direkt zu der Website navigieren (http:// _SiteCollectionName_/_catalogs/theme/15).</span><span class="sxs-lookup"><span data-stu-id="24390-p107">To access the Theme Gallery from the SharePoint user interface, on the **Site Settings** page, under **Web Designer Galleries**, choose **Themes**. You can also navigate directly to the site (http:// _SiteCollectionName_/_catalogs/theme/15/).</span></span>
    
  
- <span data-ttu-id="24390-p108">**Formatbibliothek** Führt die benutzerdefinierten CSS-Dateien auf, die Sie in der Designoberfläche verwenden möchten. Sie können direkt zur Formatbibliothek navigieren (ersetzen Sie _SiteCollectionName_ und _language_ in dieser URL: http:// _SiteCollectionName_/Style Library/ _language_/Themable/).</span><span class="sxs-lookup"><span data-stu-id="24390-p108">**Style library** Lists custom CSS files that you want to use in the theming experience. You can navigate directly to the Style library (replace _SiteCollectionName_ and _language_ in this URL: http:// _SiteCollectionName_/Style Library/ _language_/Themable/).</span></span>
    
    > <span data-ttu-id="24390-137">**Hinweis:** Legen Sie die benutzerdefinierten CSS-Dateien im Ordner „Themable“ in der Formatvorlagenbibliothek ab, nicht im Ordner „Themable“ im Gestaltungsvorlagenkatalog.</span><span class="sxs-lookup"><span data-stu-id="24390-137">**Note** Place the custom CSS files in the Themable folder in the Style library, not the Themable folder in the Master Page Gallery. Only CSS files that are stored in the Themable folder in the Style library are recognized by the theming engine.</span></span> <span data-ttu-id="24390-138">Das Designmodul erkennt ausschließlich die CSS-Dateien im Ordner „Themable“ in der Formatvorlagenbibliothek.</span><span class="sxs-lookup"><span data-stu-id="24390-138">Place the custom CSS files in the Themable folder in the Style library, not the Themable folder in the Master Page Gallery. Only CSS files that are stored in the Themable folder in the Style library are recognized by the theming engine.</span></span> 

> <span data-ttu-id="24390-139">**Hinweis:** Wenn Sie im Gestaltungsvorlagenkatalog und im Designkatalog die Versionsverwaltung aktiviert haben, müssen Sie die Designdateien außerdem zuerst veröffentlichen, damit das Designmodul sie verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="24390-139">**Note** If you have versioning enabled on the Master Page Gallery and the Theme Gallery, you must also publish the design files before they can be used by the theming engine.</span></span> 
  
    
    


## <a name="deploy-a-theme-by-using-the-user-interface"></a><span data-ttu-id="24390-140">Bereitstellen eines Designs mithilfe der Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="24390-140">Deploy a theme by using the user interface</span></span>
<span data-ttu-id="24390-141"><a name="section2"> </a></span><span class="sxs-lookup"><span data-stu-id="24390-141"></span></span>

<span data-ttu-id="24390-p110">Unter einem durchkomponierten Look oder einem Design versteht man die Farbpalette, das Schriftartenschema, das Hintergrundbild und die Gestaltungsvorlage, welche das Erscheinungsbild einer Website bestimmen. Die Liste "Durchkomponierte Looks" enthält die durchkomponierten Looks, die in der Design Gallery verfügbar sind. Sie können ein Design erstellen, indem Sie in der Liste "Durchkomponierte Looks" ein Listenelement hinzufügen und angeben, welche Gestaltungsvorlage, welche Farbpalette, welches Schriftartenschema und welches Hintergrundbild verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="24390-p110">A composed look, or design, is the color palette, font scheme, background image, and master page that determine the look and feel of a site. The Composed Looks list contains the composed looks that are available in the design gallery. You create a design by adding a list item in the Composed Looks list and specifying the master page, color palette, font scheme, and background image to use.</span></span>
  
    
    

> <span data-ttu-id="24390-145">**Hinweis:** Soll die Gestaltungsvorlage im Designkatalog verfügbar sein, benötigen Sie für die Gestaltungsvorlage eine Vorschaudatei.</span><span class="sxs-lookup"><span data-stu-id="24390-145">**Note** A master page preview file is required if you want the master page to be available in the design gallery.</span></span> 
  
    
    


### <a name="to-add-a-composed-look"></a><span data-ttu-id="24390-146">Hinzufügen eines durchkomponierten Looks</span><span class="sxs-lookup"><span data-stu-id="24390-146">To add a composed look</span></span>


1. <span data-ttu-id="24390-147">Wählen Sie das Symbol **Einstellungen** und dann **Websiteeinstellungen** aus.</span><span class="sxs-lookup"><span data-stu-id="24390-147">Choose the **Settings** icon, and then choose **Site settings**.</span></span>
    
  
2. <span data-ttu-id="24390-148">Wählen Sie unter **Web-Designer-Kataloge** **Durchkomponierte Looks** aus.</span><span class="sxs-lookup"><span data-stu-id="24390-148">Under **Web Designer Galleries**, choose **Composed looks**.</span></span>
    
  
3. <span data-ttu-id="24390-149">Wählen Sie in der Liste **Durchkomponierte Looks** **Neues Element** aus.</span><span class="sxs-lookup"><span data-stu-id="24390-149">In the **Composed Looks** list, select **new item**.</span></span>
    
  
4. <span data-ttu-id="24390-150">Geben Sie im Textfeld **Titel** einen Titel für das Design ein.</span><span class="sxs-lookup"><span data-stu-id="24390-150">In the **Title** text box, enter a title for the design.</span></span>
    
  
5. <span data-ttu-id="24390-p111">Geben Sie im Textfeld **Name** einen Namen für das Design ein. Der Name wird in der Liste "Durchkomponierte Looks" und in der Design Gallery angezeigt.</span><span class="sxs-lookup"><span data-stu-id="24390-p111">In the **Name** text box, enter a name for the design. The name appears in the Composed Looks list and in the design gallery.</span></span>
    
  
6. <span data-ttu-id="24390-p112">Geben Sie im Textfeld ** Gestaltungsvorlagen-URL** die URL der Gestaltungsvorlage ein. Die URL kann eine relative URL sein.</span><span class="sxs-lookup"><span data-stu-id="24390-p112">In the **Master Page URL** text box, enter the URL of the master page. The URL can be a relative URL.</span></span>
    
  
7. <span data-ttu-id="24390-p113">Geben Sie im Textfeld **Design-URL** die URL der Farbpalette (die URL zur .spcolor-Datei) ein. Die URL kann eine relative URL sein.</span><span class="sxs-lookup"><span data-stu-id="24390-p113">In the **Theme URL** text box, enter the URL of the color palette (the URL to the .spcolor file). The URL can be a relative URL.</span></span>
    
  
8. <span data-ttu-id="24390-p114">Geben Sie im Textfeld **Bild-URL** die URL zum Hintergrundbild ein. Dies ist optional. Die URL kann eine relative URL sein.</span><span class="sxs-lookup"><span data-stu-id="24390-p114">In the **Image URL** text box, enter the URL of the background image. This is optional. The URL can be a relative URL.</span></span>
    
  
9. <span data-ttu-id="24390-p115">Geben Sie im Textfeld **Schriftartenschema-URL** die URL des Schriftartenschemas (die URL zur .spfont-Datei) ein. Dies ist optional. Die URL kann eine relative URL sein.</span><span class="sxs-lookup"><span data-stu-id="24390-p115">In the **Font Scheme URL** text box, enter the URL of the font scheme (the URL to the .spfont file). This is optional. The URL can be a relative URL.</span></span>
    
  
10. <span data-ttu-id="24390-p116">Geben Sie im Textfeld **Anzeigereihenfolge** die Nummer der Anzeigereihenfolge ein. Hiervon hängt ab, wo das Design in der Design Gallery angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="24390-p116">In the **Display Order** text box, enter the display order number. This determines where the design appears in the design gallery.</span></span>
    
  
11. <span data-ttu-id="24390-165">Klicken Sie auf **Speichern**.</span><span class="sxs-lookup"><span data-stu-id="24390-165">Choose **Save**.</span></span>
    
    > <span data-ttu-id="24390-166">**Hinweis:** Sind die Werte des durchkomponierten Looks fehlerhaft, wird der durchkomponierte Look nicht zum Designkatalog hinzugefügt. In einem solchen Fall wird keine Meldung in die Protokolldateien geschrieben.</span><span class="sxs-lookup"><span data-stu-id="24390-166">If there is an issue with the composed look values, the composed look is not added to the design gallery, and no message is recorded in the log files. The following are possible reasons why a composed look cannot be added: a file cannot be found, there is a formatting issue with one of the files, or SharePoint is unable to access the files.</span></span> <span data-ttu-id="24390-167">Wenn ein durchkomponierter Look nicht hinzugefügt werden kann, kann das folgende Gründe haben: Eine Datei wurde nicht gefunden, in einer der Dateien gibt es Formatierungsfehler, oder SharePoint kann nicht auf die Dateien zugreifen.</span><span class="sxs-lookup"><span data-stu-id="24390-167">If there is an issue with the composed look values, the composed look is not added to the design gallery, and no message is recorded in the log files. The following are possible reasons why a composed look cannot be added: a file cannot be found, there is a formatting issue with one of the files, or SharePoint is unable to access the files.</span></span> 
      > <span data-ttu-id="24390-168">Nun können Sie das neue Design über den Designkatalog auf Ihre Website anwenden.</span><span class="sxs-lookup"><span data-stu-id="24390-168">You can now use the design gallery to apply the new design to your site. For more information, see Choose a theme for your publishing sitehttp://office.microsoft.com/de-DE/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx on Office.com.</span></span> <span data-ttu-id="24390-169">Weitere Informationen finden Sie unter [Auswählen eines Designs für Ihre Veröffentlichungswebsite](http://office.microsoft.com/de-DE/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx) auf Office.com.</span><span class="sxs-lookup"><span data-stu-id="24390-169">You can also decide to use one of the preinstalled SharePoint themes. For more information, see  [Choose a theme for your publishing site](http://office.microsoft.com/de-DE/office365-sharepoint-online-enterprise-help/choose-a-theme-for-your-publishing-site-HA102891580.aspx) on Office.com.</span></span>
  
    
    

## <a name="deploy-a-theme-by-using-code"></a><span data-ttu-id="24390-170">Bereitstellen eines Designs mithilfe von Code</span><span class="sxs-lookup"><span data-stu-id="24390-170">Deploy a theme by using code</span></span>
<span data-ttu-id="24390-171"><a name="section3"> </a></span><span class="sxs-lookup"><span data-stu-id="24390-171"></span></span>

<span data-ttu-id="24390-172">Sie können ein Design durch die Implementierung eines Featureempfängers bereitstellen.</span><span class="sxs-lookup"><span data-stu-id="24390-172">You can deploy a theme by implementing a feature receiver.</span></span>
  
    
    

### <a name="to-deploy-a-theme-by-using-a-feature-receiver"></a><span data-ttu-id="24390-173">So stellen Sie ein Design mithilfe eines Featureempfängers bereit</span><span class="sxs-lookup"><span data-stu-id="24390-173">To deploy a theme by using a feature receiver</span></span>


1. <span data-ttu-id="24390-174">Erstellen Sie eine Featureempfängerklasse, die von der  [SPFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.aspx) -Klasse erbt.</span><span class="sxs-lookup"><span data-stu-id="24390-174">Create a feature receiver class that inherits from the  [SPFeatureReceiver](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.aspx) class.</span></span>
    
  
2. <span data-ttu-id="24390-175">Erstellen Sie in der  [FeatureActivated](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.FeatureActivated.aspx) -Methode ein [SPTheme](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPTheme.aspx) -Objekt, das die Farbpalette und das Schriftartenschema verwendet, und wenden Sie das Design dann auf Ihre Website an.</span><span class="sxs-lookup"><span data-stu-id="24390-175">In the  [FeatureActivated](https://msdn.microsoft.com/library/Microsoft.SharePoint.SPFeatureReceiver.FeatureActivated.aspx) method, create an [SPTheme](https://msdn.microsoft.com/library/Microsoft.SharePoint.Utilities.SPTheme.aspx) object that uses the color palette and font scheme, and then apply the theme to your site.</span></span>
    
    <span data-ttu-id="24390-176">Das folgende Codebeispiel demonstriert, wie Sie eine benutzerdefinierte Farbpalette und ein benutzerdefiniertes Schriftartenschema auf eine Website anwenden können:</span><span class="sxs-lookup"><span data-stu-id="24390-176">The following code example shows how to deploy a custom color palette and font scheme to a site.</span></span>
    


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


## <a name="additional-resources"></a><span data-ttu-id="24390-177">Weitere Ressourcen</span><span class="sxs-lookup"><span data-stu-id="24390-177">Additional resources</span></span>
<span data-ttu-id="24390-178"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="24390-178"></span></span>


-  [<span data-ttu-id="24390-179">Entwickeln des Website-Designs in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24390-179">Develop the site design in SharePoint</span></span>](develop-the-site-design-in-sharepoint.md)
    
  
-  [<span data-ttu-id="24390-180">Farbpaletten und Schriftarten in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24390-180">Color palettes and fonts in SharePoint</span></span>](color-palettes-and-fonts-in-sharepoint.md)
    
  
-  [<span data-ttu-id="24390-181">Gewusst wie: Erstellen einer Gestaltungsvorlagen-Vorschaudatei in SharePoint</span><span class="sxs-lookup"><span data-stu-id="24390-181">How to: Create a master page preview file in SharePoint</span></span>](how-to-create-a-master-page-preview-file-in-sharepoint.md)
    
  
-  [<span data-ttu-id="24390-182">SharePoint-Teamblog: Beweisen Sie Stil mit SharePoint-Designs</span><span class="sxs-lookup"><span data-stu-id="24390-182">SharePoint Team Blog: Show off your style with SharePoint theming</span></span>](http://blogs.office.com/b/sharepoint/archive/2012/10/29/show-off-your-style-with-sharepoint-theming.aspx)
    
  

