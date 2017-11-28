---
title: Verwenden Sie remote-Bereitstellung zu Marke SharePoint-Seiten
ms.date: 11/03/2017
ms.openlocfilehash: 195d5e183850625d732ae696447cbc9a56ab1e8b
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="use-remote-provisioning-to-brand-sharepoint-pages"></a>Verwenden Sie remote-Bereitstellung zu Marke SharePoint-Seiten

Verwenden Sie remote-Bereitstellung zur Interaktion mit Designs in SharePoint.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Sie können anwenden und interagieren mit Designs mithilfe von remote provisioning Features in SharePoint. Diese Features werden durch die folgenden APIs bereitgestellt:

-  [ApplyTheme-Methode](http://msdn.microsoft.com/library/52c567e8-03e6-7ba3-a9ed-cf4e3c22dbdd%28Office.15%29.aspx)
    
-  [ThemeInfo-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx)
    
**ApplyTheme** -Methode eignet sich ideal für die Änderung der Assistent aussehen. Der Assistent gilt Acomposed Aussehen oder ein benutzerdefiniertes aussehen, für eine SharePoint-Website mithilfe der angegebene Komponenten. Designs sind Website-Website angewendet.
Die **ApplyThemeApp** und **ThemeInfo** serverseitige APIs sind über der **ApplyTheme-** und der **ThemeInfo** -APIs in CSOM und JSOM verfügbar gemacht.
Ein Beispiel, das Sie zum Anwenden einer vorhandenen oder benutzerdefinierten Designs finden Sie unter [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes) auf GitHub anzeigt.

## <a name="applytheme-method"></a>ApplyTheme-Methode
<a name="sectionSection0"> </a>

Verwenden Sie die Client-seitigen **ApplyTheme** -Methode bei Verwendung von remote-Bereitstellung Anwenden von Designs, wie im folgenden Beispiel dargestellt.

```
public void ApplyTheme(
            string colorPaletteUrl,
            string fontSchemeUrl,
            string backgroundImageUrl,
            bool shareGenerated
             )
```

**ApplyTheme** -Methode verwendet die folgenden Parameter:

- ColorPaletteUrl - die serverrelative URL der Farbpalettendatei (beispielsweise Spcolor).
    
- FontSchemeUrl - die serverrelative URL der Schriftartenschemadatei (beispielsweise Spfont).
    
- BackgroundImageUrl - die serverrelative URL des Hintergrundbilds. Wenn kein Hintergrundbild vorhanden ist, gibt dieser Parameter einen **null** -Verweis zurück.
    
- ShareGenerated - ein Boolean-Wert. **True,** Wenn die generierte Designdateien auf der Stammwebsite angewendet werden soll. **"false"** werden in der aktuellen Website gespeichert werden.

**Hinweis**  Der Parameter ShareGenerated bestimmt, ob die entsprechendes mit Design versehenes Ausgabedateien gespeichert sind, in einem Web-spezifische Speicherort oder einem Speicherort, der in der gesamten Websitesammlung zugegriffen werden kann. Es wird empfohlen, dass Sie den Standardwert für den Websitetyp beibehalten.

## <a name="themeinfo-class"></a>ThemeInfo-Klasse
<a name="sectionSection1"> </a>

CSOM-Code können Sie Informationen zu den zusammengesetzten erhalten möchten, die auf einer Website angewendet werden. Die [ThemeInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx) -Klasse dient zum Abrufen des Kontexts mit Designs, wie im folgenden Beispiel dargestellt.

```
public ThemeInfo ThemeInfo { get; }
```

Die **ThemeInfo** -Klasse können Sie Informationen zu Designs abrufen, die auf einer Website, einschließlich Beschreibungen, Kontext, Objektdaten, Farben und Schriftarten für den angegebenen Namen (und Schriftarten für die angegebene Sprachcode) sowie den URI für den Hintergrund angewendet werden Bild für zusammengesetztes Design definiert ist.

## <a name="using-applytheme-and-themeinfo-in-csom-code"></a>Verwenden von ApplyTheme- und der ThemeInfo CSOM-Code
<a name="sectionSection2"> </a>

Im folgenden Codebeispiel wird veranschaulicht, wie Sie **ApplyTheme** und **ThemeInfo** in CSOM-Code verwenden. Sie können diesen Code im remote provisioning Muster verwenden. Sie könnten beispielsweise zusammengesetzten gemäß einem Designer programmgesteuert erstellen und Bereitstellen von Websites in der Webanwendung.

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Text;
using System.IO;
using Microsoft.SharePoint.Client;

namespace ApplyThemeAppWeb.Pages
{
    public partial class Default : System.Web.UI.Page
    {
        public string _ContextToken 
        {
            get
            {
                if (ViewState["ContextToken"] == null)
                    return null;
                return ViewState["ContextToken"].ToString();
            }
            set
            {
                ViewState["ContextToken"] = value;
            }
        }

        public string _HostWeb
        {
            get
            {
                if (ViewState["HostWeb"] == null)
                    return null;
                return ViewState["HostWeb"].ToString();
            }
            set
            {
                ViewState["HostWeb"] = value;
            }
        }

        protected void Page_Load(object sender, EventArgs e)
        {
            if (!IsPostBack)
            {
                _ContextToken = TokenHelper.GetContextTokenFromRequest(Page.Request);
                _HostWeb = Page.Request["SPHostUrl"];
            }

            StatusMessage.Text = string.Empty;
        }

        protected void GetThemeInfo_Click(object sender, EventArgs e)
        {
            try
            {
                StatusMessage.Text += GetThemeInfo();
            }
            catch (Exception ex)
            {
                StatusMessage.Text += Environment.NewLine + ex.ToString();
            }
        }

        protected void ApplyTheme_Click(object sender, EventArgs e)
        {
            try
            {
                ApplyTheme();
                StatusMessage.Text += "Theme applied. Click Get Theme Info to see changes." + Environment.NewLine;
            }
            catch (Exception ex)
            {
                StatusMessage.Text += Environment.NewLine + ex.ToString();
            }
        }

        private string GetThemeInfo()
        {
            using (var clientContext = TokenHelper.GetClientContextWithContextToken(_HostWeb, _ContextToken, Request.Url.Authority))
            {

                Web hostWebObj = clientContext.Web;
                ThemeInfo initialThemeInfo = hostWebObj.ThemeInfo;

                // Get the initial theme info for the web. No need to load the entire web object.
                clientContext.Load(hostWebObj, w => w.ThemeInfo, w => w.CustomMasterUrl);

                // Theme component info is available via a method call that must be run.
                var linkShade = initialThemeInfo.GetThemeShadeByName("Hyperlink");
                var titleFont = initialThemeInfo.GetThemeFontByName("title", 1033);

                // Run.
                clientContext.ExecuteQuery();

                // Use ThemeInfo to show some data about the theme currently applied to the web.
                StringBuilder initialInfo = new StringBuilder();
                initialInfo.AppendFormat("Current master page: {0}\r\n", hostWebObj.CustomMasterUrl);
                initialInfo.AppendFormat("Background Image: {0}\r\n", initialThemeInfo.ThemeBackgroundImageUri);
                initialInfo.AppendFormat("The \"Hyperlink\" Color for this theme is: {0}\r\n", linkShade.Value);
                initialInfo.AppendFormat("The \"title\" Font for this theme is: {0}\r\n", titleFont.Value);
                return initialInfo.ToString();
            }
        }

        protected void ApplyTheme()
        {
            using (var clientContext = TokenHelper.GetClientContextWithContextToken(_HostWeb, _ContextToken, Request.Url.Authority))
            {
                // Apply the new theme.

                // First, copy theme files to a temporary location (the web's Site Assets library).
                Web hostWebObj = clientContext.Web;
                Site hostSiteObj = clientContext.Site;
                Web hostRootWebObj = hostSiteObj.RootWeb;
                
                // Get the necessary lists and libraries.
                List themeLibrary = hostRootWebObj.Lists.GetByTitle("Theme Gallery");
                Folder themeFolder = themeLibrary.RootFolder.Folders.GetByUrl("15");
                List looksGallery = hostRootWebObj.Lists.GetByTitle("Composed Looks");
                List masterLibrary = hostRootWebObj.Lists.GetByTitle("Master Page Gallery");
                List assetLibrary = hostRootWebObj.Lists.GetByTitle("Site Assets");

                clientContext.Load(themeFolder, f => f.ServerRelativeUrl);
                clientContext.Load(masterLibrary, l => l.RootFolder);
                clientContext.Load(assetLibrary, l => l.RootFolder);

                // First, upload the theme files to the Theme Gallery.
                DirectoryInfo themeDir = new DirectoryInfo(Server.MapPath("/Theme"));
                foreach (var themeFile in themeDir.EnumerateFiles())
                {
                    FileCreationInformation newFile = new FileCreationInformation();
                    newFile.Content = System.IO.File.ReadAllBytes(themeFile.FullName);
                    newFile.Url = themeFile.Name;
                    newFile.Overwrite = true;
                    
                    // Sort by file extension into the correct library. 
                    switch (themeFile.Extension)
                    {
                        case ".spcolor":
                        case ".spfont":
                            Microsoft.SharePoint.Client.File uploadTheme = themeFolder.Files.Add(newFile);
                            clientContext.Load(uploadTheme);
                            break;
                        case ".master":
                        case ".html":
                            Microsoft.SharePoint.Client.File updloadMaster = masterLibrary.RootFolder.Files.Add(newFile);
                            clientContext.Load(updloadMaster);
                            break;
                        default:
                            Microsoft.SharePoint.Client.File uploadAsset = assetLibrary.RootFolder.Files.Add(newFile);
                            clientContext.Load(uploadAsset);
                            break;
                    }

                }

                // Run the file upload.
                clientContext.ExecuteQuery();

                // Create a new composed look for the theme.
                string themeFolderUrl = themeFolder.ServerRelativeUrl;
                string masterFolderUrl = masterLibrary.RootFolder.ServerRelativeUrl;

                // Optional: Use to make the custom theme available for selection in the UI. For
          // example, for OneDrive for Business sites, you don't need this code because 
                // the ability to set a theme is hidden. 
          ListItemCreationInformation newLook = new ListItemCreationInformation();
                Microsoft.SharePoint.Client.ListItem newLookItem = looksGallery.AddItem(newLook);
                newLookItem["Title"] = "Theme Sample Look";
                newLookItem["Name"] = "Theme Sample Look";

                FieldUrlValue masterFieldValue = new FieldUrlValue();
                masterFieldValue.Url = masterFolderUrl + "/seattle.master";
                newLookItem["MasterPageUrl"] = masterFieldValue;

                FieldUrlValue colorFieldValue = new FieldUrlValue();
                colorFieldValue.Url = themeFolderUrl + "/ThemeSample.spcolor";
                newLookItem["ThemeUrl"] = colorFieldValue;

                FieldUrlValue fontFieldValue = new FieldUrlValue();
                fontFieldValue.Url = themeFolderUrl + "/ThemeSample.spfont";
                newLookItem["FontSchemeUrl"] = fontFieldValue;

                newLookItem.Update();

                // Apply the master page.
                hostWebObj.CustomMasterUrl = masterFieldValue.Url;

                // Update between the last and next steps. ApplyTheme throws errors if the theme
          // and master page are updated in the same query.
                hostWebObj.Update();
                clientContext.ExecuteQuery();

                // Apply the theme.
                hostWebObj.ApplyTheme(
                    colorFieldValue.Url, // URL of the color palette (.spcolor) file,
                    fontFieldValue.Url, // URL to the font scheme (.spfont) file (optional)
                    null, // Background Image URL (optional, null here),
                    false // false stores the composed look files in this web only. True shares the composed look with the site collection (to which you need permission). 

                // Need to call update to apply the change to the host web.
                hostWebObj.Update();

                // Run the Update method.
                clientContext.ExecuteQuery();
            }
        }
    }
}
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

-  [Lösungen für das SharePoint-Websitebranding und die Seitenanpassung](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [Verwendung zusammengesetzt sucht nach Marke SharePoint-Websites](Use-composed-looks-to-brand-SharePoint-sites.md)
    
-  [Branding.Themes-Beispiel](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes)
