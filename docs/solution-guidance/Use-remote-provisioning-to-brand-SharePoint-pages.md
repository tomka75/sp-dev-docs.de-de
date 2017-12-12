---
title: Verwenden Sie remote-Bereitstellung zu Marke SharePoint-Seiten
ms.date: 11/03/2017
ms.openlocfilehash: e06c83261af951070f37320917afcae544fbf95f
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-remote-provisioning-to-brand-sharepoint-pages"></a><span data-ttu-id="9ed39-102">Verwenden Sie remote-Bereitstellung zu Marke SharePoint-Seiten</span><span class="sxs-lookup"><span data-stu-id="9ed39-102">Use remote provisioning to brand SharePoint pages</span></span>

<span data-ttu-id="9ed39-103">Verwenden Sie remote-Bereitstellung zur Interaktion mit Designs in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9ed39-103">Use remote provisioning to interact with themes in SharePoint.</span></span>

<span data-ttu-id="9ed39-104">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="9ed39-104">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="9ed39-105">Sie können anwenden und interagieren mit Designs mithilfe von remote provisioning Features in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9ed39-105">You can apply and interact with themes by using remote provisioning features in SharePoint.</span></span> <span data-ttu-id="9ed39-106">Diese Features werden durch die folgenden APIs bereitgestellt:</span><span class="sxs-lookup"><span data-stu-id="9ed39-106">These features are provided by the following APIs:</span></span>

-  [<span data-ttu-id="9ed39-107">ApplyTheme-Methode</span><span class="sxs-lookup"><span data-stu-id="9ed39-107">ApplyTheme method</span></span>](http://msdn.microsoft.com/library/52c567e8-03e6-7ba3-a9ed-cf4e3c22dbdd%28Office.15%29.aspx)
    
-  [<span data-ttu-id="9ed39-108">ThemeInfo-Klasse</span><span class="sxs-lookup"><span data-stu-id="9ed39-108">ThemeInfo class</span></span>](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx)
    
<span data-ttu-id="9ed39-109">**ApplyTheme** -Methode eignet sich ideal für die Änderung der Assistent aussehen.</span><span class="sxs-lookup"><span data-stu-id="9ed39-109">The  **ApplyTheme** method powers the Change the Look wizard.</span></span> <span data-ttu-id="9ed39-110">Der Assistent gilt Acomposed Aussehen oder ein benutzerdefiniertes aussehen, für eine SharePoint-Website mithilfe der angegebene Komponenten.</span><span class="sxs-lookup"><span data-stu-id="9ed39-110">The wizard applies acomposed look, or a custom look, to a SharePoint site by using specified components.</span></span> <span data-ttu-id="9ed39-111">Designs sind Website-Website angewendet.</span><span class="sxs-lookup"><span data-stu-id="9ed39-111">Themes are applied on a site-by-site basis.</span></span>
<span data-ttu-id="9ed39-112">Die **ApplyThemeApp** und **ThemeInfo** serverseitige APIs sind über der **ApplyTheme-** und der **ThemeInfo** -APIs in CSOM und JSOM verfügbar gemacht.</span><span class="sxs-lookup"><span data-stu-id="9ed39-112">The  **ApplyThemeApp** and **ThemeInfo** server-side APIs are exposed via the **ApplyTheme** and **ThemeInfo** APIs in CSOM and JSOM.</span></span>
<span data-ttu-id="9ed39-113">Ein Beispiel, das Sie zum Anwenden einer vorhandenen oder benutzerdefinierten Designs finden Sie unter [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes) auf GitHub anzeigt.</span><span class="sxs-lookup"><span data-stu-id="9ed39-113">For a sample that shows you how to apply an existing or custom theme, see  [Branding.Themes](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes) on GitHub.</span></span>

## <a name="applytheme-method"></a><span data-ttu-id="9ed39-114">ApplyTheme-Methode</span><span class="sxs-lookup"><span data-stu-id="9ed39-114">ApplyTheme method</span></span>
<span data-ttu-id="9ed39-115"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="9ed39-115"></span></span>

<span data-ttu-id="9ed39-116">Verwenden Sie die Client-seitigen **ApplyTheme** -Methode bei Verwendung von remote-Bereitstellung Anwenden von Designs, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="9ed39-116">Use the  **ApplyTheme** client-side method when you use remote provisioning to apply themes, as shown in the following example.</span></span>

```
public void ApplyTheme(
            string colorPaletteUrl,
            string fontSchemeUrl,
            string backgroundImageUrl,
            bool shareGenerated
             )
```

<span data-ttu-id="9ed39-117">**ApplyTheme** -Methode verwendet die folgenden Parameter:</span><span class="sxs-lookup"><span data-stu-id="9ed39-117">The  **ApplyTheme** method uses the following parameters:</span></span>

- <span data-ttu-id="9ed39-118">ColorPaletteUrl - die serverrelative URL der Farbpalettendatei (beispielsweise Spcolor).</span><span class="sxs-lookup"><span data-stu-id="9ed39-118">colorPaletteUrl - The server-relative URL of the color palette file (for example, spcolor).</span></span>
    
- <span data-ttu-id="9ed39-119">FontSchemeUrl - die serverrelative URL der Schriftartenschemadatei (beispielsweise Spfont).</span><span class="sxs-lookup"><span data-stu-id="9ed39-119">fontSchemeUrl - The server-relative URL of the font scheme file (for example, spfont).</span></span>
    
- <span data-ttu-id="9ed39-120">BackgroundImageUrl - die serverrelative URL des Hintergrundbilds.</span><span class="sxs-lookup"><span data-stu-id="9ed39-120">backgroundImageUrl - The server-relative URL of the background image.</span></span> <span data-ttu-id="9ed39-121">Wenn kein Hintergrundbild vorhanden ist, gibt dieser Parameter einen **null** -Verweis zurück.</span><span class="sxs-lookup"><span data-stu-id="9ed39-121">If there is no background image, this parameter returns a **null** reference.</span></span>
    
- <span data-ttu-id="9ed39-122">ShareGenerated - ein Boolean-Wert.</span><span class="sxs-lookup"><span data-stu-id="9ed39-122">shareGenerated - A Boolean value.</span></span> <span data-ttu-id="9ed39-123">**True,** Wenn die generierte Designdateien auf der Stammwebsite angewendet werden soll. **"false"** werden in der aktuellen Website gespeichert werden.</span><span class="sxs-lookup"><span data-stu-id="9ed39-123">**True** if the generated theme files should be applied to the root web; **false** if they are to be stored in the current web.</span></span>

> [!NOTE] 
> <span data-ttu-id="9ed39-124">Der Parameter ShareGenerated bestimmt, ob die entsprechendes mit Design versehenes Ausgabedateien gespeichert sind, in einem Web-spezifische Speicherort oder einem Speicherort, der in der gesamten Websitesammlung zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="9ed39-124">The shareGenerated parameter determines whether the themed output files are stored in a web-specific location or a location that is accessible across the site collection.</span></span> <span data-ttu-id="9ed39-125">Es wird empfohlen, dass Sie den Standardwert für den Websitetyp beibehalten.</span><span class="sxs-lookup"><span data-stu-id="9ed39-125">We recommend that you keep the default value for your site type.</span></span>

## <a name="themeinfo-class"></a><span data-ttu-id="9ed39-126">ThemeInfo-Klasse</span><span class="sxs-lookup"><span data-stu-id="9ed39-126">ThemeInfo class</span></span>
<span data-ttu-id="9ed39-127"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="9ed39-127"></span></span>

<span data-ttu-id="9ed39-128">CSOM-Code können Sie Informationen zu den zusammengesetzten erhalten möchten, die auf einer Website angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="9ed39-128">You can use CSOM code to get information about the composed looks that are applied to a site.</span></span> <span data-ttu-id="9ed39-129">Die [ThemeInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx) -Klasse dient zum Abrufen des Kontexts mit Designs, wie im folgenden Beispiel dargestellt.</span><span class="sxs-lookup"><span data-stu-id="9ed39-129">The  [ThemeInfo](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.client.themeinfo.aspx) class gets the context associated with the themes, as shown in the following example.</span></span>

```
public ThemeInfo ThemeInfo { get; }
```

<span data-ttu-id="9ed39-130">Die **ThemeInfo** -Klasse können Sie Informationen zu Designs abrufen, die auf einer Website, einschließlich Beschreibungen, Kontext, Objektdaten, Farben und Schriftarten für den angegebenen Namen (und Schriftarten für die angegebene Sprachcode) sowie den URI für den Hintergrund angewendet werden Bild für zusammengesetztes Design definiert ist.</span><span class="sxs-lookup"><span data-stu-id="9ed39-130">You can use the  **ThemeInfo** class to get details about themes that are applied to a site, including descriptions, context, object data, colors, and fonts for the specified name (and fonts for the specified language code), as well as the URI for the background image defined for the composed look.</span></span>

## <a name="using-applytheme-and-themeinfo-in-csom-code"></a><span data-ttu-id="9ed39-131">Verwenden von ApplyTheme- und der ThemeInfo CSOM-Code</span><span class="sxs-lookup"><span data-stu-id="9ed39-131">Using ApplyTheme and ThemeInfo in CSOM code</span></span>
<span data-ttu-id="9ed39-132"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="9ed39-132"></span></span>

<span data-ttu-id="9ed39-133">Im folgenden Codebeispiel wird veranschaulicht, wie Sie **ApplyTheme** und **ThemeInfo** in CSOM-Code verwenden.</span><span class="sxs-lookup"><span data-stu-id="9ed39-133">The following code example shows how to use  **ApplyTheme** and **ThemeInfo** in CSOM code.</span></span> <span data-ttu-id="9ed39-134">Sie können diesen Code im remote provisioning Muster verwenden.</span><span class="sxs-lookup"><span data-stu-id="9ed39-134">You can use this code in the remote provisioning pattern.</span></span> <span data-ttu-id="9ed39-135">Sie könnten beispielsweise zusammengesetzten gemäß einem Designer programmgesteuert erstellen und Bereitstellen von Websites in der Webanwendung.</span><span class="sxs-lookup"><span data-stu-id="9ed39-135">For example, you might decide to create composed looks programmatically, as specified by a designer, and provision them to sites in your web application.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="9ed39-136">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="9ed39-136">See also</span></span>
<span data-ttu-id="9ed39-137"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9ed39-137"></span></span>

-  [<span data-ttu-id="9ed39-138">Lösungen für das SharePoint-Websitebranding und die Seitenanpassung</span><span class="sxs-lookup"><span data-stu-id="9ed39-138">SharePoint site branding and page customization solutions</span></span>](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [<span data-ttu-id="9ed39-139">Verwendung zusammengesetzt sucht nach Marke SharePoint-Websites</span><span class="sxs-lookup"><span data-stu-id="9ed39-139">Use composed looks to brand SharePoint sites</span></span>](Use-composed-looks-to-brand-SharePoint-sites.md)
    
-  [<span data-ttu-id="9ed39-140">Branding.Themes-Beispiel</span><span class="sxs-lookup"><span data-stu-id="9ed39-140">Branding.Themes sample</span></span>](https://github.com/Lauragra/PnP/tree/master/Samples/Branding.Themes)
