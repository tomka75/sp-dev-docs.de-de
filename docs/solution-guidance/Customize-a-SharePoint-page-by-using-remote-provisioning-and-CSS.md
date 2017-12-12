---
title: Anpassen einer SharePoint-Seite mithilfe von remote-Bereitstellung und CSS
ms.date: 11/03/2017
ms.openlocfilehash: 6cf2eb2044af5a8659e19fea94e009824e7ec9d2
ms.sourcegitcommit: 0a94e0c600db24a1b5bf5895e6d3d9681bf7c810
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2017
---
# <a name="customize-a-sharepoint-page-by-using-remote-provisioning-and-css"></a>Anpassen einer SharePoint-Seite mithilfe von remote-Bereitstellung und CSS

Verwenden Sie zum Anpassen von SharePoint-rich-Text-Felder und Webpartzonen CSS.

_**Gilt für:** Office 365 | SharePoint 2013 | SharePoint Online_

Sie können cascading Stylesheets (CSS) zum Anpassen von SharePoint-rich-Text-Felder und Webpartzonen verwenden. Informationen zum Anpassen von rich-Text-Felder, können Sie dieses Recht auf der Seite Aufgaben ausführen, die Sie bearbeiten. Sie können für Webpartzonen verwenden Sie das Skript-Editor-Webpart, um HTML oder Skripts hinzufügen oder ordnen Sie ein Cascading Stylesheet.
Ein Codebeispiel, das in diesem Artikel zugeordnet ist, finden Sie in GitHub [Branding.AlternateCSSAndSiteLogo](https://github.com/SharePoint/PnP/tree/master/Samples/Branding.AlternateCSSAndSiteLogo) in [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP) .

## <a name="customize-rich-text-fields"></a>Rich-Text-Felder anpassen
<a name="sectionSection0"> </a>

Sie können mithilfe von CSS-rechts im Editor Seite rich-Text-Felder anpassen:

1. Wählen Sie in der SharePoint-Seite **Bearbeiten** , um die Seite-Editor zu öffnen.
    
2. Wählen Sie im Menüband **Einfügen** > **Code einbetten**.
    
Sie können jetzt hinzufügen oder Ändern von CSS-Elemente für ein rich-Text-Feld.

## <a name="customize-web-part-zones"></a>Anpassen von Webpartzonen
<a name="sectionSection1"> </a>

Um Webpartzonen mit CSS anzupassen, verwenden Sie das Skript-Editor-Webpart. Weitere Informationen finden Sie unter [Gewusst wie: Verwenden des Skript-Editor-Webparts in SharePoint 2013](http://community.bamboosolutions.com/blogs/sharepoint-2013/archive/2013/05/20/how-to-use-script-editor-web-part-in-sharepoint-2013.aspx).

> [!NOTE] 
> Wenn Sie SharePoint Online und des NoScript-Features verwenden, wird das Skript-Editor-Webpart deaktiviert. 

Im folgenden Codebeispiel wird benutzerdefinierte CSS in der Ressourcenbibliothek hochgeladen, wendet einen Verweis auf die CSS-URL mit einer benutzerdefinierten Aktion und anschließend erstellt eine benutzerdefinierte Aktion, um einen Link zu der neuen CSS-Datei zu erstellen.

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

                        // First, upload the CSS files to the Asset Library.
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
                        
                        // Clean up existing actions that we may have deployed.
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

                        // Build a custom action to write a link to your new CSS file.
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
    
-  [Gewusst wie: Verwenden des Skript-Editor-Webparts in SharePoint 2013](http://community.bamboosolutions.com/blogs/sharepoint-2013/archive/2013/05/20/how-to-use-script-editor-web-part-in-sharepoint-2013.aspx)
    
-  [ScriptEditorWebPart-Klasse](https://msdn.microsoft.com/en-us/library/office/microsoft.sharepoint.webpartpages.scripteditorwebpart.aspx)
