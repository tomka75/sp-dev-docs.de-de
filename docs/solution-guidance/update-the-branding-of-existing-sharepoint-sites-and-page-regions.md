---
title: Aktualisieren Sie das branding der vorhandenen SharePoint-Websites und Bereiche der Seite
ms.date: 11/03/2017
ms.openlocfilehash: 13fc6929dfa4aedfd87bb772c3e7687f71ce135d
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="update-the-branding-of-existing-sharepoint-sites-and-page-regions"></a>Aktualisieren Sie das branding der vorhandenen SharePoint-Websites und Bereiche der Seite

Passen Sie an und aktualisieren Sie das branding von vorhandenen SharePoint-Websites und Regionen von SharePoint-Seiten, einschließlich des Menübands, der Websitenavigation, im Menü Einstellungen, die Strukturansicht und dem Seiteninhalt.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Sie können das branding auf Ihren vorhandenen SharePoint-Websites und Websitesammlungen aktualisieren sowie Bereiche von SharePoint-Seiten anpassen. Möglicherweise möchten Sie beispielsweise hierzu, wenn Sie auf der Website eine neue Version aktualisieren. 

## <a name="refresh-branding-of-existing-sites-and-subsites"></a>Aktualisieren von vorhandenen Websites und Unterwebsites branding

Im Beispiel [Branding.Refresh](https://github.com/SharePoint/PnP/tree/dev/Scenarios/Branding.Refresh) im [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) Projekt auf GitHub zeigt, wie Sie die OfficeDevPnP.Core-Bibliothek verwenden, das zum Durchlaufen der vorhandenen Websites und Unterwebsites, um zu überprüfen und Aktualisieren der angewendeten branding. Das Beispiel veranschaulicht das branding Website aktualisieren, aber dasselbe Konzept kann verwendet werden, um andere Aktionen, wie eine neue Bibliothek für eine Liste der Websites bereitstellen oder Aktualisieren einer benutzerdefinierten Aktion, die während der Bereitstellung bereitgestellt wurde. Das gleiche Verfahren können Sie um vorhandene Websites in einer neueren Version zu verschieben.

Der Vorgang umfasst zwei Schritte:

- Rufen Sie die Websites, die Sie aktualisieren möchten.
    
- Aktualisieren der Websites.

### <a name="step-one-get-the-sites-you-want-to-update"></a>Schritt 1: Abrufen der Websites, die Sie aktualisieren möchten.

Rufen Sie zunächst, eine Liste von Websites und Unterwebsites, die Sie aktualisieren möchten. Im Beispiel veranschaulicht, wie mithilfe der Suchfunktion dazu, aber andere Optionen gehören Lesen aus einem Websiteverzeichnis oder Bereitstellen ein Management Benutzeroberfläche denen Administratoren die Liste angeben können. Das folgende Beispiel veranschaulicht die Suchfunktion verwenden, um die Liste zu generieren.

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

Der Aufruf von **GetSubSites** ist rekursive, sodass es auf die Unterwebsite Struktur abruft. Nachdem die Struktur abgerufen wurde, stellen Sie sicher, dass die zurückgegebene Nummer richtig ist, bevor Sie fortfahren.

### <a name="step-two-update-the-branding"></a>Schritt 2: Aktualisieren der branding

Nachdem Sie eine Website für die Verarbeitung ausgewählt haben, können Sie OfficeDevPnP.Core Methoden zum Bearbeiten der Website verwenden. Das Beispiel zeigt, wie für das Websitebranding dazu, aber verarbeiten Sie jede Art der Änderung auf die gleiche Weise.

Das Beispiel verwendet ein Muster, das den Web-Eigenschaftenbehälter zum Speichern von Informationen zu den aktuellen Einstellungen nutzt. Der Code liest zuerst Eigenschaftensammlung Eigenschaftswerte im Web und und führt eine Aktion, die für jeden Wert geeignet ist.

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

Der Code, mit der das Design dann aktualisiert ist einfach und basiert auf OfficeDevPnP.Core-Methoden.

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

## <a name="customize-regions-of-a-sharepoint-page"></a>Anpassen von Formularbereichen einer SharePoint-Seite

Wenn Ihr Ziel ist es, Bereiche einer SharePoint-Seite anpassen, können Sie eine Kombination von remote-Bereitstellung und benutzerdefinierte cascading Stylesheets (CSS) auf Bereiche der Seite zugeordneten Dateien. Zunächst müssen Sie Ihnen bekannt sein welche SharePoint-Dateien mit den verschiedenen Bereichen einer SharePoint-Seite verknüpft sind. 

**In Tabelle 1. Bereiche der SharePoint-Seite und die zugehörigen Dateien**

|**Seite region**|** Zugeordneten Dateien **|**Weitere Informationen**|
|:-----|:-----|:-----|
|Menüband|Eine der Standardgestaltungsvorlage. Entsprechende CSS: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Haupttext - Body: #s4-Arbeitsbereich</p></li><li><p>Suite Balken - links: #suiteBarLeft</p></li><li><p>Suite Balken - rechts: #suiteBarRight</p></li><li><p>Menübandcontainer: #globalNavBox</p></li></ul>|Kann über die Schaltfläche **Inhalte zu Schwerpunktthemen** ausgeblendet werden.|
|Suitenavigation|Eine der Standardgestaltungsvorlage. |Kann über die Schaltfläche **Inhalte zu Schwerpunktthemen** ausgeblendet werden.|
|Suite-links||Kann über die Schaltfläche **Inhalte zu Schwerpunktthemen** ausgeblendet werden.|
|Willkommensmenü|Master|Kann über die Schaltfläche **Inhalte zu Schwerpunktthemen** ausgeblendet werden.|
|Im Einstellungsmenü oder Zahnrad|Master|Ein Beispiel finden Sie unter [FTC zu CAM - benutzerdefinierte Aktionen und -Eigenschaft Objektdepot Einträge aus SP-Add-in](http://blogs.msdn.com/b/vesku/archive/2013/10/02/ftc-to-cam-custom-actions-and-property-bag-entries.aspx).|
|Hilfe|Master||
|Kontextbezogene Registerkarten auf dem Menüband|Jede Standardgestaltungsvorlage.|Beispiele finden Sie unter den folgenden: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/df1e4e32-ef58-4b51-8ac8-a8c3690e648b/sharepoint-2013-duplicate-contextual-tabs?forum=sharepointdevelopment" target="_blank">SharePoint 2013 Duplikat kontextbezogene Registerkarten</a></p></li><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/a3640d58-afe1-41d0-ac83-bd7886c37355/hide-a-contextual-ribbon-tab?forum=crmdevelopment" target="_blank">Ausblenden einer kontextbezogenen Menüband-Registerkarte</a></p></li><li><p><a href="https://social.msdn.microsoft.com/Forums/sharepoint/en-US/201306cf-5874-4778-b773-f870c67cee94/hideshow-contextual-tab-on-click-event-of-subgrid?forum=crmdevelopment" target="_blank">Kontextregisterkarte einblenden/ausblenden auf klicken Sie auf Unterraster-Ereignis</a></p></li></ul>|
|Symbolleiste für den Schnellzugriff|Master|Kann über die Schaltfläche **Inhalte zu Schwerpunktthemen** ausgeblendet werden.|
|Website-logo|Master<p>Entsprechende CSS:.ms-Sitelcon-img</p>||
|Der oberen Navigationsleiste|NAV CSOM/JSOM<p>Master</p>Entsprechende CSS (nicht im Bearbeitungsmodus): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Neues Element ausgewählt:.ms-Kern-ListMenu-HorizontalBox li.static >.ms - core.listMenu-ausgewählten</p></li><li><p>Neue Artikel beim Daraufzeigen: .mscore-ListMenu-HorizontalBox li.static > a.ms-Kern-ListMenu-Element: beim Daraufzeigen</p></li><li><p>Dropdown-Pfeil:.ms-Kern-ListMenu-HorizontalBox .dynamic-children.additional-Hintergrund</p></li><li><p>Navigationselement (entsprechend der Menüelemente der obersten Ebene):.ms-Kern-ListMenu-HorizontalBox li.static >.ms-Kern-ListMenu-Element</p></li><li><p>Dropdown-Element: ul.dynamic.ms-Kern-ListMenu-Element</p></li><li><p>Dropdown-Container: ul.dynamic</p></li><li><p>Links zum Bearbeiten:.ms-Navedit-EditLinksText > span >.ms - Metadaten</p></li></ul>Entsprechende CSS (im Bearbeitungsmodus): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>NAV bearbeiten Modus Link:.ms-Kern-ListMenu-HorizontalBox.ms-Kern-ListMenuEdit > tr > .msnavedit LinkCell >.ms-Kern-ListMenu-Element</p></li><li><p>Link hinzufügen:.ms-Kern-ListMenu-HorizontalBox a.ms-Navedit-addNewLink</p></li></ul>||
|Seitentitel|Entsprechende CSS (im Bearbeitungsmodus): <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Seitentitel und Seitentitel mit Link:.ms-Kern-Seitentitel,.ms-Kern-Seitentitel ein</p></li><li><p>Schaltfläche Beschreibung: #ms-PageDescriptionDiv</p></li><li><p>Im Beschreibungsfeld: js-Popup-MainElement</p></li><li><p>Beschreibung im Feld Pfeil: js-Popup-Schnabelspitze</p></li><li><p>Beschreibung: js-Callout-Body</p></li></ul>||
|Suchfeld|NAV CSOM/JSOM<p>Master</p>Entsprechende CSS: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Suche Knotenrahmens:.ms-\endash-Sb-Rahmen</p></li><li><p>Suchen im Feld Rahmen beim Daraufzeigen:.ms-\endash-Sb-Rahmen: beim Daraufzeigen</p></li><li><p>Suchen Sie beim Klicken auf den Rahmen:.ms-\endash-Sb-BorderFocused</p></li><li><p>Feld Input Suchtextfeld:.ms-\endash-Sb-borderFocused</p></li><li><p>Suchen im Feld Text:.ms-\endash-sb</p></li><li><p>Feld Input Suchtextfeld:.ms-\endash-Sb-Suche</p></li><li><p>Suche</p></li></ul>||
|Navigationsbereich|NAV CSOM/JSOM<p>Master</p>|Weitere Informationen finden Sie unter: <ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p><a href="https://msdn.microsoft.com/en-us/library/office/ms558975(v=office.14).aspx" target="_blank">Vorgehensweise: Anpassen der Navigation in SharePoint Server</a></p></li><li><p><a href="http://msdn.microsoft.com/library/c9da5011-3c73-4b83-8e00-e7a03a71ed02(Office.15).aspx" target="_blank">Verwaltete Navigation in SharePoint 2013</a></p></li></ul>|
|Strukturansicht|Master|Weitere Informationen finden Sie unter [Vorgehensweise: Anpassen den integrierten Treeview Navigator](https://social.msdn.microsoft.com/Forums/sharepoint/en-US/dd4d49fd-e107-469d-b326-d37c86ff66b8/how-to-customize-the-builtin-treeview-navigator-?forum=sharepointcustomizationprevious).|
|Seiteninhalt|Layout/Seiteninhalten Seiten<br>Webpartzone /-Webparts<p>Entsprechende CSS (WebPartZone und Webpart):</p><ul xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:mtps="http://msdn2.microsoft.com/mtps" xmlns:mshelp="http://msdn.microsoft.com/mshelp" xmlns:ddue="http://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:msxsl="urn:schemas-microsoft-com:xslt"><li><p>Webpartzone:.ms-Webpart-zone</p></li><li><p>Webpart Inhaber:.ms-Webpartzone-Zelle</p></li><li><p>Webparttitel:.ms-Webpart-titleText</p></li><li><p>Web-Webpart-Titel mit Link:.ms-Webpart-TitleText > ein</p></li><li><p>Webpart Body:.ms-WPBody</p></li></ul>|Weitere Informationen finden Sie unter [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx)|

Beispiele im Zusammenhang mit Bereichen einer Seite anpassen finden Sie im folgenden in der [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) Projekt auf GitHub:

- [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)
    
- [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Scenarios/Branding.Themes)

### <a name="required-minimal-content-placeholders-in-default-sharepoint-master-pages"></a>"Minimale" Inhaltsplatzhalter in der standardmäßigen SharePoint-Gestaltungsvorlagen erforderlich

SharePoint Master Pages erfordern für die Verwendung von Platzhaltern für Inhalte, die die grundlegenden Content und strukturellen Elemente zu rendern, die eine SharePoint-Seite zur Unterstützung der Lebenszyklus der Seite muss. In Tabelle 2 aufgeführt und beschrieben die Inhaltsplatzhalter.

**In Tabelle 2. Mindestens erforderliche Inhaltsplatzhalter für eine SharePoint-Gestaltungsvorlage**

|**Platzhalter für Inhalt**|**Enthält Inhalt für**|
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
|PlaceHolderSiteName|Der Name der Website (Suitenavigation).|
|PlaceHolderTitleAreaClass|Der Titelbereich der Seite (Suitenavigation).|
|PlaceHolderTitleAreaSeparator|Schatten im Titelbereich (Suitenavigation).|
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

Im Allgemeinen wird empfohlen, dass Sie die [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) -Klasse zum Hinzufügen oder Entfernen von Hyperlinks und anderen Elementen verwenden. Dies ist ein Variant-Wert mit SharePoint mithilfe von [CustomAction](https://msdn.microsoft.com/en-us/library/office/ms460194.aspx) -Elements, die Sie als Teil der Feature-Framework erkennen möglicherweise, wenn Sie mit dem Objektmodell voll vertrauenswürdiger Code vertraut. Obwohl das **CustomAction** -Element und Feature Framework provisioning Muster sind insbesondere im Client-seitigen Objektmodell (CSOM) nicht unterstützt, können die gleichen Speicherort Bezeichner **CustomAction** -Elements zur Verfügung in CSOM-Code verwendet werden .

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

Wenn Sie das Menüband anpassen, wird der HTML-Code, die der Server rendert der Klassenname zugewiesen, die eine benutzerdefinierte Formatvorlage zugewiesen. Verwenden Sie dieses Feature, wechseln in die Formatbibliothek, und erstellen eine neue CSS-Datei für jede Formatvorlage, die Sie im Menüband hinzufügen möchten. Sie können benutzerdefinierte Formate zwei Abschnitte des Menübands hinzufügen: **Seitenelemente** und **Textarten.** Verwenden Sie die folgende Syntax für die Formate, die Sie hinzufügen:

- Für die ** Seite Elemente ** Abschnitt: `span.ms-rteElement-<yourowndefinedname>`. Alternativ können Sie die Formatvorlagen H1, H2, H3 oder H4, die den Text umbrochen werden, die auf die Formatvorlage angewendet wird.
    
- Für den Abschnitt **Textarten** : `.ms-rteEStyle-<yourowndefinedname>`.
    
Fügen Sie dann in der CSS-Klassendefinition die folgende Zeile: 

`-ms-name:"The name visual in the ribbon for your style";`

Sie können jetzt abgeschlossen, definieren die Details zu Ihrer benutzerdefinierten CSS-Klasse in Ihrer benutzerdefinierten CSS-Datei.

### <a name="customize-suite-navigation-on-a-web-part-page"></a>Anpassen der Suite Navigation auf einer Webpartseite

In SharePoint 2013 hat die Benutzeroberfläche einer modernen Aussehen und Verhalten, die auf der Seite Kacheln basiert. Beispielsweise werden Live Kacheln auf der Standardseite für SharePoint 2013 standardmäßig angezeigt. Der oberen Navigationsleiste erleichtert es Benutzern, anzuzeigen und Zugriff auf soziale Inhalte und OneDrive für Unternehmen. Sie können das Aussehen und Verhalten dieser Bereiche mithilfe einer Mischung aus CSS- und JavaScript anpassen.

Nach der Erstellung einer Webpartseite fügen Sie ein Skript-Editor Web Part (SEWP hinzu) eine Webpartzone verfügbar. In diesem Webpart können Sie JavaScript zu einer Seite hinzufügen. Sie können die SEWP JavaScript-Code hinzufügen, die die oberen Navigationsleiste durch seine **ElementId**identifiziert und dann ausblenden, indem Sie die Visibility-Eigenschaft auf ausgeblendete festlegen.

### <a name="customize-the-settings-menu-or-gear"></a>Anpassen der im Menü Einstellungen oder Zahnrad

Einträge Eigenschaftensammlung [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) -Klasse und -Eigenschaft können Sie von einer beliebigen SharePoint-Website im Einstellungsmenü anpassen, wie im folgenden Codebeispiel dargestellt.

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

### <a name="customize-the-tree-view"></a>Anpassen der Strukturansicht

Um die Breite der Strukturansicht zu ändern, Hinzufügen einer `<div>` markieren, um das Tag Struktur in die master-Seite, und weisen Sie eine CSS-Klasse mit einer Formatvorlage Breite-Attribut die `<div>`. Sie können die Breite des **der schnellstartnavigation** erhöhen, indem Sie die CSS-Datei die folgenden Formatvorlagendefinition hinzufügen.

```
.ms-nav {
  width: 220 px;
}
```

### <a name="customize-page-content"></a>Anpassen von Seiteninhalten

Anforderungen für das Anpassen von Seiteninhalten richten sich nach den Inhalt, den Sie auf der Seite aufnehmen möchten. Wie bei anpassen im Menü **Websiteaktionen** , können Sie ein [UserCustomAction](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.usercustomaction.aspx) -Objekt branding mit Webparts bereit.

Wenn Sie eine Veröffentlichungswebsite erstellen, finden Sie unter [Vorgehensweise: Erstellen eines Seitenlayouts in SharePoint 2013](http://msdn.microsoft.com/library/5447e6a1-2f14-4667-81d0-7514b468be80%28Office.15%29.aspx) zu die Grundlagen vertraut zu machen. Seitenlayouts hängen die Verfügbarkeit der [ContentTypeId](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.contenttypeid.aspx) -Klasse in CSOM. Wie bei anderen Elementen, die in CSOM nicht verfügbar sind, können Sie einen Windows Communication Foundation (WCF)-Dienst **ContentTypeId** als vorübergehende Lösung entwickelt.

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Lösungen für das SharePoint-Websitebranding und die Seitenanpassung](SharePoint-site-branding-and-page-customization-solutions.md)
    
- [Branding und Bereitstellen von Lösungen für SharePoint 2013 und SharePoint Online-Website](Branding-and-site-provisioning-solutions-for-SharePoint.md)
