---
title: Verwenden von CSS zum Branding von SharePoint-Seiten
ms.date: 11/03/2017
ms.openlocfilehash: b491e21a1b96d9d2843b092e763b5d45835e2e5d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-css-to-brand-sharepoint-pages"></a><span data-ttu-id="f97f4-102">Verwenden von CSS zum Branding von SharePoint-Seiten</span><span class="sxs-lookup"><span data-stu-id="f97f4-102">Use CSS to brand SharePoint pages</span></span>
<span data-ttu-id="f97f4-103">Verwenden Sie CSS, um Branding und Websitedesign in SharePoint zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="f97f4-103">Use CSS to support branding and site design in SharePoint.</span></span> <span data-ttu-id="f97f4-104">Erfahren Sie mehr über CSS in Masterseiten, die Datei "corev15.css" und zusammengesetzte Designs in benutzerdefiniertem Branding.</span><span class="sxs-lookup"><span data-stu-id="f97f4-104">Find out about CSS is master pages, the corev15.css file, and composed looks in custom branding.</span></span>

<span data-ttu-id="f97f4-105">_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="f97f4-105">_**Applies to:** Office 365 | SharePoint 2013 | SharePoint Online_</span></span>

<span data-ttu-id="f97f4-106">Cascading Stylesheets (CSS) spielt beim SharePoint-Branding eine große Rolle.</span><span class="sxs-lookup"><span data-stu-id="f97f4-106">Cascading style sheet (CSS) plays a large role in SharePoint branding.</span></span> <span data-ttu-id="f97f4-107">Um das Websitedesign in SharePoint 2013 und SharePoint Online erfolgreich anzupassen, ist es sinnvoll, dass Sie sich damit vertraut machen, wie SharePoint CSS verwendet.</span><span class="sxs-lookup"><span data-stu-id="f97f4-107">To successfully customize the site design in SharePoint 2013 and SharePoint Online, it's useful to be familiar with how SharePoint uses CSS.</span></span>

## <a name="css-branding-overview"></a><span data-ttu-id="f97f4-108">Übersicht über CSS-Branding</span><span class="sxs-lookup"><span data-stu-id="f97f4-108">CSS branding overview</span></span>
<span data-ttu-id="f97f4-109"><a name="sectionSection0"> </a></span><span class="sxs-lookup"><span data-stu-id="f97f4-109"></span></span>

<span data-ttu-id="f97f4-110">Beim Erstellen einer SharePoint -Websitesammlung erstellt SharePoint einen Gestaltungsvorlagenkatalog (_catalogs/masterpage), in dem die meisten Brandindressurcen, einschließlich MASTER-, CSS, Bild-, HTML- und JavaScript-Dateien, gespeichert sind.</span><span class="sxs-lookup"><span data-stu-id="f97f4-110">When you create a SharePoint site collection, SharePoint creates a Master Page Gallery (_catalogs/masterpage) where most branding assets, including .master, .css, image, HTML, and JavaScript files are stored.</span></span>

<span data-ttu-id="f97f4-111">In SharePoint 2013 verwendet SharePoint die Seite „seattle.master“ für Teamwebsites, Veröffentlichungswebsites und Teamwebsites mit aktivierter Veröffentlichung.</span><span class="sxs-lookup"><span data-stu-id="f97f4-111">In SharePoint 2013, SharePoint uses the seattle.master page by default for Team sites, Publishing sites, and Team sites with Publishing enabled.</span></span> <span data-ttu-id="f97f4-112">„mysite15.master“ wird für OneDrive for Business-Websites verwendet.</span><span class="sxs-lookup"><span data-stu-id="f97f4-112">It uses mysite15.master for OneDrive for Business sites.</span></span> <span data-ttu-id="f97f4-113">Jede Master-Datei verweist auf die Datei „corev15.css“, die aus einer Vielzahl von CSS-Dateien besteht, die standardmäßig in SharePoint enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="f97f4-113">Each .master file refers to the corev15.css file, which is built from a variety of .css files delivered with SharePoint out of the box.</span></span>

<span data-ttu-id="f97f4-114">Alle Standard-Masterseiten verwenden "corev15.css" beim Verarbeiten von Formatvorlagen und basieren auf der CSS-Überlappung und die CSS-Dateifreigabe, um zu lösen, welche Formatvorlagen auf bestimmte Steuerelemente und Elemente in Abschnitten einer Seite angewendet werden.</span><span class="sxs-lookup"><span data-stu-id="f97f4-114">All default master pages use corev15.css when processing styles, and rely on the CSS cascade and CSS file sharing to resolve which styles are applied to specific controls and elements in regions of a page.</span></span> <span data-ttu-id="f97f4-115"> Es werden auch mehrere CSS-Dateien kombiniert, woraus die Datei „oslo.css“ entsteht, die mit der oslo.master-Masterseite verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f97f4-115">Multiple CSS files are also combined to build the oslo.css file, which is used with the oslo.master master page.</span></span>

## <a name="css-in-master-pages"></a><span data-ttu-id="f97f4-116">CSS auf Masterseiten</span><span class="sxs-lookup"><span data-stu-id="f97f4-116">CSS in master pages</span></span>
<span data-ttu-id="f97f4-117"><a name="sectionSection1"> </a></span><span class="sxs-lookup"><span data-stu-id="f97f4-117"></span></span>

<span data-ttu-id="f97f4-118">Der `<SharePoint:CssRegistration>`-Inhaltsplatzhalter, der der [WebControls.CssRegistration]((https://msdn.microsoft.com/de-DE/library/office/microsoft.sharepoint.webcontrols.cssregistration.aspx))-Klasse im serverseitigen Objektmodell entspricht, definiert die CSS-Datei.</span><span class="sxs-lookup"><span data-stu-id="f97f4-118">The  `<SharePoint:CssRegistration>` content placeholder, which corresponds to the [WebControls.CssRegistration]((https://msdn.microsoft.com/de-DE/library/office/microsoft.sharepoint.webcontrols.cssregistration.aspx)) class in the server-side object model, defines the CSS file.</span></span> <span data-ttu-id="f97f4-119">Wie ein Verweis auf eine Masterseite ersetzt SharePoint die Token in der Masterseite, wenn die Seite verarbeitet wird.</span><span class="sxs-lookup"><span data-stu-id="f97f4-119">Like a reference to a master page, SharePoint replaces the tokens in the master page when the page is processed.</span></span> <span data-ttu-id="f97f4-120">Die [WebControls.CssLink]((https://msdn.microsoft.com/de-DE/library/office/microsoft.sharepoint.webcontrols.csslink.aspx))-Klasse liest die Registrierung aus der Masterseite und fügt ein `<link>`-Tag in die resultierende HTML-Datei ein, die generiert wird.</span><span class="sxs-lookup"><span data-stu-id="f97f4-120">The [WebControls.CssLink]((https://msdn.microsoft.com/de-DE/library/office/microsoft.sharepoint.webcontrols.csslink.aspx)) class reads the registration from the master page and inserts a `<link>` tag in the resulting HTML file that is generated.</span></span>

<span data-ttu-id="f97f4-121">Sehen Sie sich das folgende Beispiel an:</span><span class="sxs-lookup"><span data-stu-id="f97f4-121">Consider the following:</span></span>

```
<SharePoint:CssRegistration name="<% $SPUrl:~SiteCollection/Style Library/~language/Core Styles/contoso.css%>" runat="server"/>
```

<span data-ttu-id="f97f4-122">Dieser Code wird zur Laufzeit wie folgt dargestellt.</span><span class="sxs-lookup"><span data-stu-id="f97f4-122">At runtime, this code is rendered as follows.</span></span>

```
<link rel="stylesheet" type="text/css" href="/sites/nopub/Style%20Library/en-US/Core%20Styles/contoso.css">
```

<span data-ttu-id="f97f4-123">Die **CSSLink**-Klasse rendert alle Formatvorlagen, wenn die Seite gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="f97f4-123">The  **CSSLink** class renders all style sheets when the page is rendered.</span></span> <span data-ttu-id="f97f4-124">Wenn Sie Formatvorlagen in einer benutzerdefinierten CSS-Datei definieren, die auch in „corev15.css“ definiert sind, werden diese überschrieben.</span><span class="sxs-lookup"><span data-stu-id="f97f4-124">If you define styles in a custom .css file that are also defined in corev15.css, they are overwritten.</span></span>

## <a name="corev15css-file"></a><span data-ttu-id="f97f4-125">Datei „Corev15.css“</span><span class="sxs-lookup"><span data-stu-id="f97f4-125">Corev15.css file</span></span>
<span data-ttu-id="f97f4-126"><a name="sectionSection2"> </a></span><span class="sxs-lookup"><span data-stu-id="f97f4-126"></span></span>

<span data-ttu-id="f97f4-127">Standardmäßig werden zahlreiche CSS auf SharePoint angewendet.</span><span class="sxs-lookup"><span data-stu-id="f97f4-127">A lot of CSS is applied to SharePoint by default.</span></span> <span data-ttu-id="f97f4-128">Die Datei „corev15.css“ ist die Hauptquelle für Formatvorlagen in SharePoint.</span><span class="sxs-lookup"><span data-stu-id="f97f4-128">The corev15.css file is the main source for styles in SharePoint.</span></span> <span data-ttu-id="f97f4-129">Diese Datei wird im SharePoint 15-Ordner auf dem Server unter ` \TEMPLATE\LAYOUTS\1033\STYLES\Themable\COREV15.CSS` gespeichert und nicht im Gestaltungsvorlagenkatalog der Stammwebsite und Startseite.</span><span class="sxs-lookup"><span data-stu-id="f97f4-129">This file is stored in the SharePoint 15 folder on the server at ` \TEMPLATE\LAYOUTS\1033\STYLES\Themable\COREV15.CSS` and not in the Master Page Gallery of the root site and home page.</span></span>

<span data-ttu-id="f97f4-130">Sehen Sie sich die Datei „corev15.css“ mithilfe der Entwicklertools in Ihrem Webbrowser an, um zu verstehen, wie SharePoint CSS standardmäßig verwendet.</span><span class="sxs-lookup"><span data-stu-id="f97f4-130">To see how SharePoint uses CSS out of the box, look at the corev15.css file by using the developer tools in your web browser.</span></span> <span data-ttu-id="f97f4-131">Verwenden Sie in Internet Explorer die Internet Explorer-Symbolleiste für Entwickler (indem Sie die Taste **F12** drücken), und wählen Sie die Registerkarte **CSS** aus, um „corev15.css“ anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f97f4-131">In Internet Explorer, use the Internet Explorer Developer Toolbar (access it by pressing  **F12**) and choose the  **CSS** tab to view corev15.css.</span></span>

<span data-ttu-id="f97f4-132">Die in „corev15.css“ definierten Formatvorlagen verwenden die Präfixe MS und S4, die Formatvorlagen angeben, die von Microsoft erstellt wurden.</span><span class="sxs-lookup"><span data-stu-id="f97f4-132">Styles defined in corev15.css use the .ms- , and .s4- prefixes, which indicate styles that were created by Microsoft.</span></span> <span data-ttu-id="f97f4-133">„corev15.css“ verwendet auch viele untergeordnete Selektoren.</span><span class="sxs-lookup"><span data-stu-id="f97f4-133">Corev15.css also uses a lot of child and descendent selectors.</span></span> 

<span data-ttu-id="f97f4-134">Wenn Sie die Datei anzeigen, werden Sie feststellen, dass viele Kommentare das folgende Format aufweisen: `/* [ReplaceFont ( themeFont:"body")] */`.</span><span class="sxs-lookup"><span data-stu-id="f97f4-134">When you view the file, you'll notice many comments in this format:  `/* [ReplaceFont ( themeFont:"body")] */`.</span></span> <span data-ttu-id="f97f4-135">SharePoint liest diese Kommentare, wenn ein zusammengesetztes Design angewendet wird.</span><span class="sxs-lookup"><span data-stu-id="f97f4-135">SharePoint reads these comments when a composed look is applied.</span></span> <span data-ttu-id="f97f4-136">Über die Kommentare wird SharePoint angewiesen, das Attribut der CSS zu ändern, die unmittelbar auf den Kommentar folgt.</span><span class="sxs-lookup"><span data-stu-id="f97f4-136">The comments tell SharePoint to change the attribute of the CSS that immediately follows the comment.</span></span> <span data-ttu-id="f97f4-137">Durch Anwenden eines zusammengesetzten Erscheinungsbilds werden möglicherweise viele der Standardfarben, Schriftarten und Hintergrundbilder geändert, die angewendet werden, und folglich die Einstellungen in „corev15.css“ aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="f97f4-137">Applying a composed look might change many of the default colors, fonts, and background images that are applied, and subsequently update the settings in corev15.css.</span></span>

> [!NOTE] 
> <span data-ttu-id="f97f4-138">Durch Auswählen der Datei „corev15.css“ auf diese Weise wird die gerenderte CSS und nicht die gespeicherte CSS geladen.</span><span class="sxs-lookup"><span data-stu-id="f97f4-138">Selecting the corev15.css file this way loads the rendered CSS rather than the saved CSS.</span></span> <span data-ttu-id="f97f4-139">Manchmal finden Sie möglicherweise Unterschiede zwischen diesen beiden.</span><span class="sxs-lookup"><span data-stu-id="f97f4-139">Sometimes you might find discrepancies between the two.</span></span> <span data-ttu-id="f97f4-140">Benutzer-Agents wie Browser können das Rendern als Reaktion auf Benutzeraktionen ändern.</span><span class="sxs-lookup"><span data-stu-id="f97f4-140">User agents such as browsers can also change rendering in response to user actions.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="f97f4-141">Melden Sie sich nicht beim Server an, und bearbeiten oder passen Sie keine Kern-CSS-Dateien von SharePoint am SharePoint-Stamm an.</span><span class="sxs-lookup"><span data-stu-id="f97f4-141">Do not log on to the server and edit or customize core SharePoint CSS files in the SharePoint root.</span></span> <span data-ttu-id="f97f4-142">Dies hat negative Auswirkungen auf den Support und das Upgrade.</span><span class="sxs-lookup"><span data-stu-id="f97f4-142">Doing so will negatively impact support and upgrade.</span></span> <span data-ttu-id="f97f4-143">Bearbeiten Sie die Datei „corev15.css“ nie direkt; erstellen Sie immer eine Kopie, benennen Sie diese auf, und bearbeiten Sie stattdessen die neue Datei.</span><span class="sxs-lookup"><span data-stu-id="f97f4-143">Never edit the corev15.css directly; always create a copy, rename it, and edit the new file instead.</span></span> <span data-ttu-id="f97f4-144">Durch Bearbeiten von „corev15.css“ wird das Branding auf alle Webanwendungen auf dem Server angewendet.</span><span class="sxs-lookup"><span data-stu-id="f97f4-144">Editing corev15.css will apply branding to all web applications on the server.</span></span>

### <a name="to-create-a-custom-style-sheet-for-sharepoint"></a><span data-ttu-id="f97f4-145">So erstellen Sie eine benutzerdefinierte Formatvorlage für SharePoint</span><span class="sxs-lookup"><span data-stu-id="f97f4-145">To create a custom style sheet for SharePoint</span></span>

1. <span data-ttu-id="f97f4-146">Erstellen Sie eine Kopie von „corev15.css“, und nennen Sie sie „contosov15.css“.</span><span class="sxs-lookup"><span data-stu-id="f97f4-146">Make a copy of corev15.css and name it contosov15.css.</span></span>
    
2. <span data-ttu-id="f97f4-147">Öffnen Sie "contosov15.css", und ändern Sie die Zeile "CssRegistration" so, dass sie auf "contosov15.css" von "corev15.css" zeigt, wie im folgenden Beispiel gezeigt.</span><span class="sxs-lookup"><span data-stu-id="f97f4-147">Open contosov15.css and modify the CssRegistration line to point to contosov15.css from corev15.css, as shown in the following example.</span></span>
    
  ```
  <SharePoint:CssRegistration Name="Themable/contoso.css" runat="server" />
  ```

3. <span data-ttu-id="f97f4-148">Fügen Sie unterhalb der Zeile "CssRegistration" Folgendes hinzu.</span><span class="sxs-lookup"><span data-stu-id="f97f4-148">Below the CssRegistration line, add the following.</span></span>
    
  ```
  <SharePoint:CssRegistration name="/_catalogs/masterpage/contoso/contoso.css" 
runat="server">

  ```

## <a name="composed-looks-in-custom-branding"></a><span data-ttu-id="f97f4-149">Zusammengesetzte Designs in benutzerdefiniertem Branding</span><span class="sxs-lookup"><span data-stu-id="f97f4-149">Composed looks in custom branding</span></span>
<span data-ttu-id="f97f4-150"><a name="sectionSection3"> </a></span><span class="sxs-lookup"><span data-stu-id="f97f4-150"></span></span>

<span data-ttu-id="f97f4-151">Sie können zusammengesetzte Designs in benutzerdefiniertem Branding verwenden, wenn CSS von einer Masterseite aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="f97f4-151">You can use composed looks in custom branding when CSS is called from a master page.</span></span> <span data-ttu-id="f97f4-152">Die CSS-Datei wird im SharePoint-Dateisystem an einem der folgenden Speicherorte gespeichert:</span><span class="sxs-lookup"><span data-stu-id="f97f4-152">The CSS file is stored in the SharePoint file system in one of the following locations:</span></span> 

-  `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable`
    
-  `/Style Library/Themable/`
    
-  `/Style Library/{culture}/Themable/`
    
<span data-ttu-id="f97f4-153">Sie können Dateien für benutzerdefiniertes Branding in `/Style Library/Themable/` und `/Style Library/{culture}/Themable/` platzieren, `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable` kann jedoch nicht bearbeitet werden. Sie können daher keine benutzerdefinierten Dateien an diesem Ort speichern.</span><span class="sxs-lookup"><span data-stu-id="f97f4-153">You can place custom branding files in  `/Style Library/Themable/` and `/Style Library/{culture}/Themable/`, but  `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable` is not editable, so you can't store custom files in that location.</span></span>

> [!NOTE] 
> <span data-ttu-id="f97f4-154">Wenn diese Speicherorte standardmäßig nicht vorhanden sind, können Sie sie manuell erstellen; diese werden dann von SharePoint erkannt.</span><span class="sxs-lookup"><span data-stu-id="f97f4-154">If these locations don't exist by default, you can create them manually and SharePoint will recognize them as themable.</span></span>

## <a name="applying-custom-css-to-a-sharepoint-page"></a><span data-ttu-id="f97f4-155">Anwenden von benutzerdefiniertem CSS auf eine SharePoint-Seite</span><span class="sxs-lookup"><span data-stu-id="f97f4-155">Applying custom CSS to a SharePoint page</span></span>
<span data-ttu-id="f97f4-156"><a name="sectionSection4"> </a></span><span class="sxs-lookup"><span data-stu-id="f97f4-156"></span></span>

<span data-ttu-id="f97f4-157">Sie können benutzerdefinierte CSS zu Rich-Text-Felder und Webpartzonen hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="f97f4-157">You can add custom CSS to rich text fields and Web Part zones.</span></span> <span data-ttu-id="f97f4-158">Um CSS zu einem Rich-Text-Feld hinzuzufügen, setzen Sie die Seite in den Bearbeitungsmodus, und wählen Sie **Einfügen** > **Code einbetten** im Menüband aus.</span><span class="sxs-lookup"><span data-stu-id="f97f4-158">To add CSS to a rich text field, put the page in edit mode and choose  **Insert** > **Embed Code** from the ribbon.</span></span> <span data-ttu-id="f97f4-159">Verwenden Sie für Webpartzonen das Skript-Editor-Webpart, um HTML, Skripts oder eine interne Formatvorlage hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="f97f4-159">For Web Part zones, use the Script Editor Web Part to add HTML, scripts, or an internal style sheet.</span></span> <span data-ttu-id="f97f4-160">Sie können diesen Ansatz verwenden, um die Navigation über den Schnellstartbereich in der standardmäßigen SharePoint-Benutzeroberfläche auszublenden.</span><span class="sxs-lookup"><span data-stu-id="f97f4-160">You can use this approach to hide the Quick Launch navigation in the default SharePoint UI.</span></span> <span data-ttu-id="f97f4-161">Wenn Sie SharePoint Online und das Feature „NoScript“ verwenden, deaktiviert NoScript das Skript-Editor-Webpart.</span><span class="sxs-lookup"><span data-stu-id="f97f4-161">If you are using SharePoint Online and the NoScript feature, NoScript will disable Script Editor Web Part.</span></span>

<span data-ttu-id="f97f4-162">Wenden Sie CSS auf eine SharePoint -Website mithilfe einer externen Formatvorlage hinzu, und fügen Sie einen Verweis zu der Formatvorlage im `<link>`-Tag innerhalb der `<head>`-Tags der SharePoint-Seite ein.</span><span class="sxs-lookup"><span data-stu-id="f97f4-162">Apply CSS to a SharePoint site by using an external style sheet and including a reference to the style sheet in the  `<link>` tag inside the `<head>` tags of the SharePoint page.</span></span>

<span data-ttu-id="f97f4-163">Im folgenden Codebeispiel wird veranschaulicht, wie benutzerdefiniertes CSS in die Objektbibliothek hochgeladen, ein Verweis auf die CSS-URL mit einer benutzerdefinierten Aktion angewendet und dann eine benutzerdefinierte Aktion zum Erstellen eines Links zu der neuen CSS-Datei erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="f97f4-163">The following code example shows how to upload custom CSS to the asset library, apply a reference to the CSS URL with a custom action, and then create a custom action to build a link to the new CSS file.</span></span> <span data-ttu-id="f97f4-164">Dieser Code ist Teil des [Branding.AlternateCSSAndSiteLogo]((https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo))-Beispiels auf GitHub.</span><span class="sxs-lookup"><span data-stu-id="f97f4-164">This code is part of the  [Branding.AlternateCSSAndSiteLogo ]((https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo)) sample on GitHub.</span></span>

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using System.IO;
using Microsoft.SharePoint.Client;
using Microsoft.SharePoint.Client.EventReceivers;

namespace AlternateCSSAppAutohostedWeb.Services
{
    public class AppEventReceiver : IRemoteEventService
    {
        public SPRemoteEventResult ProcessEvent(SPRemoteEventProperties properties)
        {
            SPRemoteEventResult result = new SPRemoteEventResult();

            try
            {
                using (ClientContext clientContext = TokenHelper.CreateAppEventClientContext(properties, false))
                {
                    if (clientContext != null)
                    {
                        Web hostWebObj = clientContext.Web;

                        List assetLibrary = hostWebObj.Lists.GetByTitle("Site Assets");
                        clientContext.Load(assetLibrary, l => l.RootFolder);

                        // First, upload the CSS files to the Asset library.
                        DirectoryInfo themeDir = new DirectoryInfo(System.Web.Hosting.HostingEnvironment.ApplicationPhysicalPath + "CSS");
                        foreach (var themeFile in themeDir.EnumerateFiles())
                        {
                            FileCreationInformation newFile = new FileCreationInformation();
                            newFile.Content = System.IO.File.ReadAllBytes(themeFile.FullName);
                            newFile.Url = themeFile.Name;
                            newFile.Overwrite = true;

                            Microsoft.SharePoint.Client.File uploadAsset = assetLibrary.RootFolder.Files.Add(newFile);
                            clientContext.Load(uploadAsset);
                            break;
                        }
                        
                        string actionName = "SampleCSSLink";

                        // Now, apply a reference to the CSS URL via a custom action.
                        
                        // Clean up existing actions that you might have deployed.
                        var existingActions = hostWebObj.UserCustomActions;
                        clientContext.Load(existingActions);

                        // Run uploads and initialize the existing Actions collection.
                        clientContext.ExecuteQuery();

                        // Clean up existing actions.
                        foreach (var existingAction in existingActions)
                        {
                            if(existingAction.Name.Equals(actionName, StringComparison.InvariantCultureIgnoreCase))
                                existingAction.DeleteObject();
                        }
                        clientContext.ExecuteQuery();

                        // Build a custom action to write a link to our new CSS file.
                        UserCustomAction cssAction = hostWebObj.UserCustomActions.Add();
                        cssAction.Location = "ScriptLink";
                        cssAction.Sequence = 100;
                        cssAction.ScriptBlock = @"document.write('<link rel=""stylesheet"" href=""" + assetLibrary.RootFolder.ServerRelativeUrl + @"/cs-style.css"" />');";
                        cssAction.Name = actionName;
                        
                        // Apply.
                        cssAction.Update();
                        clientContext.ExecuteQuery();
                    }
                    result.Status = SPRemoteEventServiceStatus.Continue;
                    return result;
                }
            }
            catch (Exception ex)
            {
                result.Status = SPRemoteEventServiceStatus.CancelWithError;
                result.ErrorMessage = ex.Message;
                return result;
            }
            
        }

        public void ProcessOneWayEvent(SPRemoteEventProperties properties)
        {
            // This method is not used by app events.
        }
    }
}
```

## <a name="see-also"></a><span data-ttu-id="f97f4-165">Siehe auch</span><span class="sxs-lookup"><span data-stu-id="f97f4-165">See also</span></span>
<span data-ttu-id="f97f4-166"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="f97f4-166"></span></span>

-  [<span data-ttu-id="f97f4-167">Lösungen für das SharePoint-Websitebranding und die Seitenanpassung</span><span class="sxs-lookup"><span data-stu-id="f97f4-167">SharePoint site branding and page customization solutions</span></span>](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  <span data-ttu-id="f97f4-168">[Branding.AlternateCSSAndSiteLogo-Beispiel]((https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo))</span><span class="sxs-lookup"><span data-stu-id="f97f4-168">[Branding.AlternateCSSAndSiteLogo sample]((https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo))</span></span>
