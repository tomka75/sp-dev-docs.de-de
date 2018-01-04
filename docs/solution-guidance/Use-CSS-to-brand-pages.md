---
title: Verwenden von CSS zum Branding von SharePoint-Seiten
ms.date: 11/03/2017
ms.openlocfilehash: b491e21a1b96d9d2843b092e763b5d45835e2e5d
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="use-css-to-brand-sharepoint-pages"></a>Verwenden von CSS zum Branding von SharePoint-Seiten
Verwenden Sie CSS, um Branding und Websitedesign in SharePoint zu unterstützen. Erfahren Sie mehr über CSS in Masterseiten, die Datei "corev15.css" und zusammengesetzte Designs in benutzerdefiniertem Branding.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Cascading Stylesheets (CSS) spielt beim SharePoint-Branding eine große Rolle. Um das Websitedesign in SharePoint 2013 und SharePoint Online erfolgreich anzupassen, ist es sinnvoll, dass Sie sich damit vertraut machen, wie SharePoint CSS verwendet.

## <a name="css-branding-overview"></a>Übersicht über CSS-Branding
<a name="sectionSection0"> </a>

Beim Erstellen einer SharePoint -Websitesammlung erstellt SharePoint einen Gestaltungsvorlagenkatalog (_catalogs/masterpage), in dem die meisten Brandindressurcen, einschließlich MASTER-, CSS, Bild-, HTML- und JavaScript-Dateien, gespeichert sind.

In SharePoint 2013 verwendet SharePoint die Seite „seattle.master“ für Teamwebsites, Veröffentlichungswebsites und Teamwebsites mit aktivierter Veröffentlichung. „mysite15.master“ wird für OneDrive for Business-Websites verwendet. Jede Master-Datei verweist auf die Datei „corev15.css“, die aus einer Vielzahl von CSS-Dateien besteht, die standardmäßig in SharePoint enthalten sind.

Alle Standard-Masterseiten verwenden "corev15.css" beim Verarbeiten von Formatvorlagen und basieren auf der CSS-Überlappung und die CSS-Dateifreigabe, um zu lösen, welche Formatvorlagen auf bestimmte Steuerelemente und Elemente in Abschnitten einer Seite angewendet werden.  Es werden auch mehrere CSS-Dateien kombiniert, woraus die Datei „oslo.css“ entsteht, die mit der oslo.master-Masterseite verwendet wird.

## <a name="css-in-master-pages"></a>CSS auf Masterseiten
<a name="sectionSection1"> </a>

Der `<SharePoint:CssRegistration>`-Inhaltsplatzhalter, der der [WebControls.CssRegistration]((https://msdn.microsoft.com/de-DE/library/office/microsoft.sharepoint.webcontrols.cssregistration.aspx))-Klasse im serverseitigen Objektmodell entspricht, definiert die CSS-Datei. Wie ein Verweis auf eine Masterseite ersetzt SharePoint die Token in der Masterseite, wenn die Seite verarbeitet wird. Die [WebControls.CssLink]((https://msdn.microsoft.com/de-DE/library/office/microsoft.sharepoint.webcontrols.csslink.aspx))-Klasse liest die Registrierung aus der Masterseite und fügt ein `<link>`-Tag in die resultierende HTML-Datei ein, die generiert wird.

Sehen Sie sich das folgende Beispiel an:

```
<SharePoint:CssRegistration name="<% $SPUrl:~SiteCollection/Style Library/~language/Core Styles/contoso.css%>" runat="server"/>
```

Dieser Code wird zur Laufzeit wie folgt dargestellt.

```
<link rel="stylesheet" type="text/css" href="/sites/nopub/Style%20Library/en-US/Core%20Styles/contoso.css">
```

Die **CSSLink**-Klasse rendert alle Formatvorlagen, wenn die Seite gerendert wird. Wenn Sie Formatvorlagen in einer benutzerdefinierten CSS-Datei definieren, die auch in „corev15.css“ definiert sind, werden diese überschrieben.

## <a name="corev15css-file"></a>Datei „Corev15.css“
<a name="sectionSection2"> </a>

Standardmäßig werden zahlreiche CSS auf SharePoint angewendet. Die Datei „corev15.css“ ist die Hauptquelle für Formatvorlagen in SharePoint. Diese Datei wird im SharePoint 15-Ordner auf dem Server unter ` \TEMPLATE\LAYOUTS\1033\STYLES\Themable\COREV15.CSS` gespeichert und nicht im Gestaltungsvorlagenkatalog der Stammwebsite und Startseite.

Sehen Sie sich die Datei „corev15.css“ mithilfe der Entwicklertools in Ihrem Webbrowser an, um zu verstehen, wie SharePoint CSS standardmäßig verwendet. Verwenden Sie in Internet Explorer die Internet Explorer-Symbolleiste für Entwickler (indem Sie die Taste **F12** drücken), und wählen Sie die Registerkarte **CSS** aus, um „corev15.css“ anzuzeigen.

Die in „corev15.css“ definierten Formatvorlagen verwenden die Präfixe MS und S4, die Formatvorlagen angeben, die von Microsoft erstellt wurden. „corev15.css“ verwendet auch viele untergeordnete Selektoren. 

Wenn Sie die Datei anzeigen, werden Sie feststellen, dass viele Kommentare das folgende Format aufweisen: `/* [ReplaceFont ( themeFont:"body")] */`. SharePoint liest diese Kommentare, wenn ein zusammengesetztes Design angewendet wird. Über die Kommentare wird SharePoint angewiesen, das Attribut der CSS zu ändern, die unmittelbar auf den Kommentar folgt. Durch Anwenden eines zusammengesetzten Erscheinungsbilds werden möglicherweise viele der Standardfarben, Schriftarten und Hintergrundbilder geändert, die angewendet werden, und folglich die Einstellungen in „corev15.css“ aktualisiert.

> [!NOTE] 
> Durch Auswählen der Datei „corev15.css“ auf diese Weise wird die gerenderte CSS und nicht die gespeicherte CSS geladen. Manchmal finden Sie möglicherweise Unterschiede zwischen diesen beiden. Benutzer-Agents wie Browser können das Rendern als Reaktion auf Benutzeraktionen ändern.

> [!IMPORTANT] 
> Melden Sie sich nicht beim Server an, und bearbeiten oder passen Sie keine Kern-CSS-Dateien von SharePoint am SharePoint-Stamm an. Dies hat negative Auswirkungen auf den Support und das Upgrade. Bearbeiten Sie die Datei „corev15.css“ nie direkt; erstellen Sie immer eine Kopie, benennen Sie diese auf, und bearbeiten Sie stattdessen die neue Datei. Durch Bearbeiten von „corev15.css“ wird das Branding auf alle Webanwendungen auf dem Server angewendet.

### <a name="to-create-a-custom-style-sheet-for-sharepoint"></a>So erstellen Sie eine benutzerdefinierte Formatvorlage für SharePoint

1. Erstellen Sie eine Kopie von „corev15.css“, und nennen Sie sie „contosov15.css“.
    
2. Öffnen Sie "contosov15.css", und ändern Sie die Zeile "CssRegistration" so, dass sie auf "contosov15.css" von "corev15.css" zeigt, wie im folgenden Beispiel gezeigt.
    
  ```
  <SharePoint:CssRegistration Name="Themable/contoso.css" runat="server" />
  ```

3. Fügen Sie unterhalb der Zeile "CssRegistration" Folgendes hinzu.
    
  ```
  <SharePoint:CssRegistration name="/_catalogs/masterpage/contoso/contoso.css" 
runat="server">

  ```

## <a name="composed-looks-in-custom-branding"></a>Zusammengesetzte Designs in benutzerdefiniertem Branding
<a name="sectionSection3"> </a>

Sie können zusammengesetzte Designs in benutzerdefiniertem Branding verwenden, wenn CSS von einer Masterseite aufgerufen wird. Die CSS-Datei wird im SharePoint-Dateisystem an einem der folgenden Speicherorte gespeichert: 

-  `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable`
    
-  `/Style Library/Themable/`
    
-  `/Style Library/{culture}/Themable/`
    
Sie können Dateien für benutzerdefiniertes Branding in `/Style Library/Themable/` und `/Style Library/{culture}/Themable/` platzieren, `15\TEMPLATE\LAYOUTS\{LCID}\STYLES\Themable` kann jedoch nicht bearbeitet werden. Sie können daher keine benutzerdefinierten Dateien an diesem Ort speichern.

> [!NOTE] 
> Wenn diese Speicherorte standardmäßig nicht vorhanden sind, können Sie sie manuell erstellen; diese werden dann von SharePoint erkannt.

## <a name="applying-custom-css-to-a-sharepoint-page"></a>Anwenden von benutzerdefiniertem CSS auf eine SharePoint-Seite
<a name="sectionSection4"> </a>

Sie können benutzerdefinierte CSS zu Rich-Text-Felder und Webpartzonen hinzufügen. Um CSS zu einem Rich-Text-Feld hinzuzufügen, setzen Sie die Seite in den Bearbeitungsmodus, und wählen Sie **Einfügen** > **Code einbetten** im Menüband aus. Verwenden Sie für Webpartzonen das Skript-Editor-Webpart, um HTML, Skripts oder eine interne Formatvorlage hinzuzufügen. Sie können diesen Ansatz verwenden, um die Navigation über den Schnellstartbereich in der standardmäßigen SharePoint-Benutzeroberfläche auszublenden. Wenn Sie SharePoint Online und das Feature „NoScript“ verwenden, deaktiviert NoScript das Skript-Editor-Webpart.

Wenden Sie CSS auf eine SharePoint -Website mithilfe einer externen Formatvorlage hinzu, und fügen Sie einen Verweis zu der Formatvorlage im `<link>`-Tag innerhalb der `<head>`-Tags der SharePoint-Seite ein.

Im folgenden Codebeispiel wird veranschaulicht, wie benutzerdefiniertes CSS in die Objektbibliothek hochgeladen, ein Verweis auf die CSS-URL mit einer benutzerdefinierten Aktion angewendet und dann eine benutzerdefinierte Aktion zum Erstellen eines Links zu der neuen CSS-Datei erstellt wird. Dieser Code ist Teil des [Branding.AlternateCSSAndSiteLogo]((https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo))-Beispiels auf GitHub.

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

## <a name="see-also"></a>Siehe auch
<a name="bk_addresources"> </a>

-  [Lösungen für das SharePoint-Websitebranding und die Seitenanpassung](SharePoint-site-branding-and-page-customization-solutions.md)
    
-  [Branding.AlternateCSSAndSiteLogo-Beispiel]((https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo))
