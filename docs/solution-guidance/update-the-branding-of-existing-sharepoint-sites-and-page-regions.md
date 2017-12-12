---
title: Update the branding of existing SharePoint sites and page regions
ms.date: 11/03/2017
ms.openlocfilehash: 16a4e6aa21f267c008660837b765e2bd2e47a940
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="update-the-branding-of-existing-sharepoint-sites-and-page-regions"></a>Update the branding of existing SharePoint sites and page regions

Customize and then refresh the branding of existing SharePoint sites or regions of SharePoint pages, including the ribbon, the site navigation, the Settings menu, the tree view, and the page content.

_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_

You can refresh the branding on your existing SharePoint sites and site collections, as well as customize regions of SharePoint pages. You might want to do this, for example, when you update to a new version of the site. 

## <a name="refresh-branding-of-existing-sites-and-subsites"></a>Refresh branding of existing sites and subsites

The [Branding.Refresh](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Branding.Refresh) sample in the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub shows you how to use the OfficeDevPnP.Core library to iterate over existing sites and subsites to verify and update the applied branding. The sample shows how to update site branding, but the same concept can be used to do other things, such as deploy a new library to a list of sites, or update a custom action that was deployed during provisioning. You can use the same process to move existing sites to a newer version.

The operation involves two steps:

- Get the sites you want to update.
    
- Update the sites.

### <a name="step-one-get-the-sites-you-want-to-update"></a>Step one: Get the sites you want to update

First, get a list of sites and subsites that you want to update. The sample shows how to do this by using the search functionality, but other options include reading from a site directory, or providing a management UI where administrators can specify the list. The following example shows you how to use search functionality to generate the list.

```
// Get a list of sites. Search is one way to get this list, an alternative can be a site directory.
List<SiteEntity> sites = cc.Web.SiteSearchScopedByUrl("https://bertonline.sharepoint.com");

// Generic settings (apply changes on all webs or just root web).
bool applyChangesToAllWebs = true;

// Optionally further refine the list of returned site collections.
var filteredSites = from p in sites
                    where p.Url.Contains("13003")
                    select p;

List<SiteEntity> sitesAndSubSites = new List<SiteEntity>();
if (applyChangesToAllWebs)
{
  // You want to update all sites, so the list of sites is extended to all subsites.
  foreach (SiteEntity site in filteredSites)
  {
    sitesAndSubSites.Add(new SiteEntity() { Url = site.Url, 
                                            Title = site.Title, 
                                            Template = site.Template });
    GetSubSites(cc, site.Url, ref sitesAndSubSites);
  }
  sites = sitesAndSubSites;
}
```

The call to  **GetSubSites** is recursive so it fetches the subsite tree. After the tree has been fetched, verify that the number returned is correct before you continue.

### <a name="step-two-update-the-branding"></a>Step two: Update the branding

After you select a site for processing, you can use OfficeDevPnP.Core methods to manipulate the site. The sample shows how to do this for site branding, but you can process any type of change in the same way.

The sample uses a pattern that leverages the web property bag to store information about the current settings. The code first reads the web property bag values and then takes an action that is appropriate for each value.

```
// Verify that you have a property bag entry.
string themeName = cc.Web.GetPropertyBagValueString(BRANDING_THEME, "");

if (!String.IsNullOrEmpty(themeName))
{
  // If no theme property bag entry, assume no theme has been applied.
  if (themeName.Equals(currentThemeName, StringComparison.InvariantCultureIgnoreCase))
  {
    // The applied theme matches to the theme you want to update.
    int? brandingVersion = cc.Web.GetPropertyBagValueInt(BRANDING_VERSION, 0);
    if (brandingVersion < currentBrandingVersion)
    {
      DeployTheme(cc, currentThemeName);
      // Set the web propertybag entries
      cc.Web.SetPropertyBagValue(BRANDING_THEME, currentThemeName);
      cc.Web.SetPropertyBagValue(BRANDING_VERSION, currentBrandingVersion);
    }
  }
  else
  {
    if (forceBranding)
    {
      DeployTheme(cc, currentThemeName);
      // Set the web propertybag entries.
      cc.Web.SetPropertyBagValue(BRANDING_THEME, currentThemeName);
      cc.Web.SetPropertyBagValue(BRANDING_VERSION, currentBrandingVersion);
    }
  }
}
```

The code that then updates the theme is straightforward and is based on OfficeDevPnP.Core methods.

```
string themeRoot = Path.Combine(AppRootPath, String.Format(@"Themes\{0}", themeName));
string spColorFile = Path.Combine(themeRoot, string.Format("{0}.spcolor", themeName));
string spFontFile = Path.Combine(themeRoot, string.Format("{0}.spfont", themeName));
string backgroundFile = Path.Combine(themeRoot, string.Format("{0}bg.jpg", themeName));
string logoFile = Path.Combine(themeRoot, string.Format("{0}logo.png", themeName));

if (IsThisASubSite(cc.Url))
{
  // Retrieve the context of the root site of the site collection.
  using (ClientContext ccParent = new ClientContext(GetRootSite(cc.Url)))
  {
    ccParent.Credentials = cc.Credentials;
    cc.Web.DeployThemeToSubWeb(ccParent.Web, themeName, spColorFile, spFontFile, backgroundFile, "");
    cc.Web.SetThemeToSubWeb(ccParent.Web, themeName);
  }
}
else
{
  cc.Web.DeployThemeToWeb(themeName, spColorFile, spFontFile, backgroundFile, "");
  cc.Web.SetThemeToWeb(themeName);
}
```

## <a name="customize-regions-of-a-sharepoint-page"></a>Customize regions of a SharePoint page

When your objective is to customize regions of a SharePoint page, you can use a combination of remote provisioning and custom cascading style sheets (CSS) on files associated with regions of the page. Initially, then, you must be aware of which SharePoint files are associated with the various regions of a SharePoint page. 

**Table 1. SharePoint page regions and associated files**

|**Page region**|**Associated files **|**Weitere Informationen**|
|:-----|:-----|:-----|
|Menüband|Any of the default master pages. Corresponding CSS: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Main body - body: #s4-workspace</p></li><li><p>Suite bar - Left: #suiteBarLeft</p></li><li><p>Suite bar - Right: #suiteBarRight</p></li><li><p>Ribbon container: #globalNavBox</p></li></ul>|Can be hidden via the  **Focus on Content** button.|
|Suite navigation|Any of the default master pages. |Can be hidden via the  **Focus on Content** button.|
|Suite links||Can be hidden via the  **Focus on Content** button.|
|Welcome menu|Master|Kann über die Schaltfläche **Inhalte zu Schwerpunktthemen** ausgeblendet werden.|
|Settings menu or gear|Master|For an example, see [FTC to CAM - Custom actions and property bag entries from SP Add-in](http://blogs.msdn.com/b/vesku/archive/2013/10/02/ftc-to-cam-custom-actions-and-property-bag-entries.aspx).|
|Hilfe|Master||
|Ribbon contextual tabs|Any default master page.|For examples, see the following: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/df1e4e32-ef58-4b51-8ac8-a8c3690e648b/sharepoint-2013-duplicate-contextual-tabs?forum=sharepointdevelopment" target="_blank">SharePoint 2013 Duplicate Contextual Tabs</a></p></li><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/a3640d58-afe1-41d0-ac83-bd7886c37355/hide-a-contextual-ribbon-tab?forum=crmdevelopment" target="_blank">Hide a Contextual ribbon tab</a></p></li><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/201306cf-5874-4778-b773-f870c67cee94/hideshow-contextual-tab-on-click-event-of-subgrid?forum=crmdevelopment" target="_blank">Hide/Show contextual tab on click event of subgrid</a></p></li></ul>|
|Quick access toolbar|Master|Can be hidden via the  **Focus on Content** button.|
|Site logo|Master<p>Entsprechende CSS:.ms-Sitelcon-img</p>||
|Top navigation|Nav CSOM/JSOM<p>Master</p>Entsprechende CSS (nicht im Bearbeitungsmodus): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>New Item selected: .ms-core-listMenu-horizontalBox li.static > .ms-core.listMenu-selected</p></li><li><p>New Item Hover: .mscore-listMenu-horizontalBox li.static > a.ms-core-listMenu-item:hover</p></li><li><p>Flyout Arrow: .ms-core-listMenu-horizontalBox .dynamic-children.additional-background</p></li><li><p>Nav Item (corresponding to top-level menu items): .ms-core-listMenu-horizontalBox li.static > .ms-core-listMenu-item</p></li><li><p>Flyout Item: ul.dynamic .ms-core-listMenu-item</p></li><li><p>Flyout Container: ul.dynamic</p></li><li><p>Edit Links: .ms-navedit-editLinksText > span> .ms-metadata</p></li></ul>Corresponding CSS (in edit mode): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Nav Edit Mode Link: .ms-core-listMenu-horizontalBox .ms-core-listMenuEdit > tr> .msnavedit-linkCell > .ms-core-listMenu-item</p></li><li><p>Add Link: .ms-core-listMenu-horizontalBox a.ms-navedit-addNewLink</p></li></ul>||
|Seitentitel|Entsprechende CSS (im Bearbeitungsmodus): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Page Title and Page Title with Link: .ms-core-pageTitle, .ms-core-pageTitle a</p></li><li><p>Description button: #ms-pageDescriptionDiv</p></li><li><p>Description box: .js-callout-mainElement</p></li><li><p>Description box arrow: .js-callout-beak</p></li><li><p>Description text: .js-callout-body</p></li></ul>||
|Search box|Nav CSOM/JSOM<p>Master</p>Corresponding CSS: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Search Box Border: .ms-srch-sb-border</p></li><li><p>Search Box Border Hover: .ms-srch-sb-border: hover</p></li><li><p>Search Box Border when clicked: .ms-srch-sb-borderFocused</p></li><li><p>Search Box Input Text Box: .ms-srch-sb-borderFocused</p></li><li><p>Search Box Body: .ms-srch-sb</p></li><li><p>Search Box Input Text Box: .ms-srch-sb-searching</p></li><li><p>Suche</p></li></ul>||
|Left navigation|Nav CSOM/JSOM<p>Master</p>|For more information see: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms558975(v=office.14).aspx" target="_blank">How to: Customize Navigation in SharePoint Server</a></p></li><li><p><a href="http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02(Office.15).aspx" target="_blank">Managed navigation in SharePoint 2013</a></p></li></ul>|
|Tree view|.master|For more information, see [How to customize the built-in Treeview navigator](https://social.msdn.microsoft.com/Forums/sharepoint/en-US/dd4d49fd-e107-469d-b326-d37c86ff66b8/how-to-customize-the-builtin-treeview-navigator-?forum=sharepointcustomizationprevious).|
|Page content|Page Layout/Content Pages<br>Web Part Zone/Web Parts<p>Corresponding CSS (Web Part Zone and Web Part):</p><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Web Part Zone: .ms-webpart-zone</p></li><li><p>Web Part Holder: .ms-webpartzone-cell</p></li><li><p>Web Part Title: .ms-webpart-titleText</p></li><li><p>Web Part Title with Link: .ms-webpart-titleText > a</p></li><li><p>Web Part Body: .ms-WPBody</p></li></ul>|For more information, see [How to: Create a page layout in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx)|

For samples related to customizing regions of a page, see the following in the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub:

- [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
    
- [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Scenarios/Branding.Themes)

### <a name="required-minimal-content-placeholders-in-default-sharepoint-master-pages"></a>Required "minimal" content placeholders in default SharePoint master pages

SharePoint .master pages require that you use content placeholders, which render the basic content and structural elements that a SharePoint page needs to support the page lifecycle. Table 2 lists and describes the content placeholders.

**Table 2. Minimum required content placeholders for a SharePoint master page**

|**Content placeholder**|**Holds content for**|
|:-----|:-----|
|PlaceHolderAdditionalPageHead|Zusätzliche Elemente in der <head> eine Seite im Abschnitt.|
|PlaceHolderBodyAreaClass|Zusätzliche Formatvorlagen in der Kopfzeile.|
|PlaceHolderBodyLeftBorder|Die linke Rahmenlinie-Element für den Textkörper der Seite.|
|PlaceHolderBodyRightBorder|Die rechte Rahmenlinie-Element für den Textkörper der Seite.|
|PlaceHolderCalendarNavigator|Eine Datumsauswahl zum Navigieren in einem Kalender, wenn ein Kalender auf einer Seite sichtbar ist.|
|PlaceHolderFormDigest|Das "Formulardigest" Security-Steuerelement.|
|PlaceHolderGlobalNavigation|Die globale Navigation Breadcrumb (Navigation oben).|
|PlaceHolderGlobalNavigationSiteMap|Die Siteübersicht in der globalen Navigation (Navigation oben).|
|PlaceHolderHorizontalNav|Der oberen Navigationsleiste im Menü für eine Seite (Navigation oben).|
|PlaceHolderLeftActions|Unten links Navigationsbereich (Navigationsbereich links).|
|PlaceHolderLeftNavBar|Im linken Navigationsbereich (Navigationsbereich links).|
|PlaceHolderLeftNavBarDataSource|Die Datenquelle für das linke Navigationsmenü (Navigationsbereich links).|
|PlaceHolderLeftNavBarTop|Im oberen linken Navigationsbereich (Navigationsbereich links).|
|PlaceHolderMain|Der Hauptinhalt auf der Seite (Seiteninhalt).|
|PlaceHolderMiniConsole|Seitenebenen-Befehle wie Seite bearbeiten, Verlauf und eingehende Hyperlinks in ein Unternehmenswiki-Seite.|
|PlaceHolderNavSpacer|Die Breite der im linken Navigationsbereich (Navigationsbereich links).|
|Placeholderpagedescription:|Beschreibung des Seiteninhalts.|
|"PlaceHolderPageImage"|Seitensymbol in der linken oberen Ecke der Seite (im Menüband).|
|Placeholderpagetitle:|Titel der Seite (&lt;Titel&gt;) (Seitentitel) in der Titelleiste der Browserseite angezeigt.|
|PlaceHolderPageTitleInTitle|Der Seitentitel (Titel) unmittelbar unterhalb der Breadcrumb dargestellt. |
|PlaceHolderQuickLaunchBottom|Ende der schnellstartnavigation (Navigation oben).|
|PlaceHolderQuickLaunchTop|Oberen Rand der schnellstartnavigation (Navigation oben).|
|"PlaceHolderSearchArea"|Der Bereich, in dem Feld für die Suche Steuerelement, angezeigt wird (Suchfeld).|
|PlaceHolderSiteName|The name of the site (Suite Navigation).|
|PlaceHolderTitleAreaClass|The title area of the page (Suite Navigation).|
|PlaceHolderTitleAreaSeparator|Shadows in the title area (Suite Navigation).|
|PlaceHolderTitleBreadCrumb|Content Breadcrumb Titelbereich. |
|PlaceHolderTitleLeftBorder|Am linken Seitenrand Titelbereich (Suitenavigation).|
|PlaceHolderTitleRightMargin|Der rechte Rand der Titelbereich (Suitenavigation).|
|PlaceHolderTopNavBar|Der obere Navigationsbereich (Navigation oben).|
|PlaceHolderUtilities|Zusätzliche Inhalte muss, die am unteren Rand der Seite (Seiteninhalt) angezeigt werden.|
|SPNavigation|Navigation-Vorgänge enthält.|
|WSSDesignConsole|Die Seite Bearbeitungssteuerelementen, wenn die Seite im Bearbeitungsmodus befindet.|

Wenn Sie einen der Platzhalter für die Inhalte aus einer SharePoint-Seite Master in Tabelle 2 aufgelisteten entfernen, wird SharePoint ein Fehler ausgelöst. Sie können einen Inhaltsplatzhalter mit ausgeblendeten Sichtbarkeit hinzufügen, die den Inhalt von Endbenutzern verborgen.

Weitere Informationen finden Sie unter [Windows SharePoint Services Default Master Pages](https://msdn.microsoft.com/en-us/library/office/ms467402%28v=office.12%29.aspx) (in diesem Artikel werden die Funktionen in SharePoint Services 3, aber immer noch der Inhalt gilt). Siehe auch [Arbeiten mit Inhaltsplatzhalter-Steuerelemente](https://support.office.com/en-us/article/Working-with-content-placeholder-controls-d8b87b85-d1ef-409d-a5c7-044890f89288?CorrelationId=517ec37c-89ef-40d9-b70e-54aa63ac994f&amp;ui=en-US&amp;rs=en-US&amp;ad=US).

Standard-SharePoint-Gestaltungsvorlagen, wie seattle.master und oslo.master enthalten viele weitere Inhalte Platzhalter als SharePoint erfordert. Beispielsweise diesen Masterseiten enthalten `<SharePoint:Themes runat="server">` und `<SharePoint.CssRegistration runat="server">` Steuerelemente.

**Designs** und **CssRegistration** -Steuerelemente, die während der Lebenszyklus der Seite ausgeführt werden. Mit dem remote provisioning Muster, können Sie eine benutzerdefinierte Aktion zum Hinzufügen eines Steuerelements Server zum Registrieren des benutzerdefinierten CSS.

Platzhalter für Inhalte, die nicht sichtbar sind erwartungsgemäß funktionieren, aber alle Inhalte, die sie generieren wird in der HTML-Quelle, die Browser erkennen ausgelassen. Platzhalter für Inhalt mit `Visible="false"` ist ausgeblendet.

**Wichtig:**  Erstellen Sie benutzerdefinierte Platzhalter nicht in benutzerdefinierten Gestaltungsvorlagen, die in Out-of-Box-Masterseiten wie Seattle.master und Oslo.master vorhanden sind. Dadurch wird nach einem schwerwiegenden Fehler Ausnahmen.

### <a name="sharepoint-online-suite-navigation-control"></a>SharePoint Online Suite Navigations-Steuerelement

SharePoint Online stellt neue gestaltungsvorlagenmarkup für das Steuerelement **Suitenavigation** , in der oberen Navigationsleiste rendert. Standard-Markup für das Steuerelement **Suitenavigation** unterscheidet sich je nachdem, ob die Website eine Intranet- oder öffentlich zugängliche ist. Erfahren mehr über das Navigationssteuerelement **Suite** und finden Sie unter Codebeispiele für Intranet- und öffentlich zugängliche Websites, die Sie Ihrer Gestaltungsvorlagen hinzufügen können, finden Sie unter [SharePoint Online Suite Navigations-Steuerelement](http://msdn.microsoft.com/library/ba93e5c0-e591-48d0-a716-a08ec7ef6cea%28Office.15%29.aspx).

### <a name="use-csom-to-customize-the-regions-of-a-sharepoint-page"></a>Verwenden Sie CSOM zum Anpassen von Regionen einer SharePoint-Seite

Im Allgemeinen wird empfohlen, dass Sie die [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) -Klasse zum Hinzufügen oder Entfernen von Hyperlinks und anderen Elementen verwenden. Dies ist ein Variant-Wert mit SharePoint mithilfe von [CustomAction](https://msdn.microsoft.com/en-us/library/office/ms460194.aspx) -Elements, die Sie als Teil der Feature-Framework erkennen möglicherweise, wenn Sie mit dem Objektmodell voll vertrauenswürdiger Code vertraut. Although the **CustomAction** element and feature framework provisioning pattern are not specifically supported in the client-side object model (CSOM), the same location identifiers available to the **CustomAction** element can be used in CSOM code.

```
<CustomAction
  RequiredAdmin = "Delegated | Farm | Machine"
  ControlAssembly = "Text"
  ControlClass = "Text"
  ControlSrc = "Text"
  Description = "Text"
  FeatureId = "Text"
  GroupId = "Text"
  Id = "Text"
  ImageUrl = "Text"
  Location = "Text"
  RegistrationId = "Text"
  RegistrationType = "Text"
  RequireSiteAdministrator = "TRUE" | "FALSE"
  Rights = "Text"
  RootWebOnly = "TRUE" | "FALSE"
  ScriptSrc = "Text"
  ScriptBlock = "Text"
  Sequence = "Integer"
  ShowInLists = "TRUE" | "FALSE"
  ShowInReadOnlyContentTypes = "TRUE" | "FALSE"
  ShowInSealedContentTypes = "TRUE" | "FALSE"
  Title = "Text"
  UIVersion = "Integer">
</CustomAction>
```

### <a name="customize-the-sharepoint-ribbon"></a>Anpassen des Menübands für SharePoint

When you customize the ribbon, the HTML that the server renders is assigned to the class name that you assign to a custom style. To use this feature, go to the Style Library and create a new CSS file for each style that you want to add to the ribbon. Sie können benutzerdefinierte Formate zwei Abschnitte des Menübands hinzufügen: **Seitenelemente** und **Textarten.** Verwenden Sie die folgende Syntax für die Formate, die Sie hinzufügen:

- Für die ** Seite Elemente ** Abschnitt: `span.ms-rteElement-<yourowndefinedname>`. Alternativ können Sie die Formatvorlagen H1, H2, H3 oder H4, die den Text umbrochen werden, die auf die Formatvorlage angewendet wird.
    
- For the  **Text Styles** section: `.ms-rteEStyle-<yourowndefinedname>`.
    
Then, in your CSS class definition, add the following line: 

`-ms-name:"The name visual in the ribbon for your style";`

Now you can finish defining the details of your custom CSS class in your custom .css file.

### <a name="customize-suite-navigation-on-a-web-part-page"></a>Anpassen der Suite Navigation auf einer Webpartseite

In SharePoint 2013, the UI has a modern look and feel that is based on page tiles. For example, Live Tiles appear on the default SharePoint 2013 page by default. Der oberen Navigationsleiste erleichtert es Benutzern, anzuzeigen und Zugriff auf soziale Inhalte und OneDrive für Unternehmen. You can customize the look and feel of these areas by using a mix of CSS and JavaScript.

After you create a Web Part page, add a Script Editor Web Part (SEWP) to an available Web Part zone. You can use this Web Part to add JavaScript to your page. You can add JavaScript code to the SEWP that identifies the top navigation bar by its  **ElementId**, and then hide it by setting its visibility property to hidden.

### <a name="customize-the-settings-menu-or-gear"></a>Customize the Settings menu or gear

You can use the [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) class and property bag entries to customize the settings menu of any SharePoint site, as shown in the following code example.

```
public void AddCustomActions(ClientContext clientContext)
{
    // Add a site settings link if it doesn't already exist.
    if (!CustomActionAlreadyExists(clientContext, "Sample_CustomSiteSetting"))
    {
        // Add a site settings link.
        UserCustomAction siteSettingLink = clientContext.Web.UserCustomActions.Add();
        siteSettingLink.Group = "SiteTasks";
        siteSettingLink.Location = "Microsoft.SharePoint.SiteSettings";
        siteSettingLink.Name = "Sample_CustomSiteSetting";
        siteSettingLink.Sequence = 1000;
        siteSettingLink.Url = string.Format(DeployManager.appUrl, clientContext.Url);
        siteSettingLink.Title = "Modify Site Metadata";
        siteSettingLink.Update();
        clientContext.ExecuteQuery();
    }

    // Add a site actions link, if it doesn't already exist.
    if (!CustomActionAlreadyExists(clientContext, "Sample_CustomAction"))
    {
        UserCustomAction siteAction = clientContext.Web.UserCustomActions.Add();
        siteAction.Group = "SiteActions";
        siteAction.Location = "Microsoft.SharePoint.StandardMenu";
        siteAction.Name = "Sample_CustomAction";
        siteAction.Sequence = 1000;
        siteAction.Url = string.Format(DeployManager.appUrl, clientContext.Url); ;
        siteAction.Title = "Modify Site Metadata";
        siteAction.Update();
        clientContext.ExecuteQuery();
    }
}
```

### <a name="customize-the-tree-view"></a>Customize the tree view

To modify the width of the tree view, add a  `<div>` tag around the tree tag in the .master page and assign a CSS class with a style width attribute to the `<div>`. You can increase the width of the  **Quick Launch** navigation by adding the following style definition to the .css file.

```
.ms-nav {
  width: 220 px;
}
```

### <a name="customize-page-content"></a>Customize page content

Requirements for customizing page content depend on the content you're including in your page. As for customizing the  **Site Actions** menu, you can use a [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) object to provision branding to Web Parts.

If you are building a publishing site, see [How to: Create a page layout in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx) to learn the basics. Page layouts depend on the availability of the [ContentTypeId](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.contenttypeid.aspx) class in CSOM. As for other members that aren't available in CSOM, you can use a Windows Communication Foundation (WCF) service to work with **ContentTypeId** as a temporary workaround.

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

- [Lösungen für das SharePoint-Websitebranding und die Seitenanpassung](SharePoint-site-branding-and-page-customization-solutions.md)
    
- [Branding and site provisioning solutions for SharePoint 2013 and SharePoint Online](Branding-and-site-provisioning-solutions-for-SharePoint.md)
