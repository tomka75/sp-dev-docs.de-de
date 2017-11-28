---
title: Hochladen von Webparts in SharePoint
ms.date: 11/03/2017
ms.openlocfilehash: c7e6e7a4bc6d843661ecd7c27d71381f47254ca9
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="upload-web-parts-in-sharepoint"></a>Hochladen von Webparts in SharePoint

Bereitstellen Sie vorkonfigurierte, standardmäßigen SharePoint-Webparts für die Benutzer.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Sie können die vorkonfigurierte, standardmäßigen SharePoint-Webparts für Benutzer hinzufügen zu ihrer SharePoint-Websites hochladen. Beispielsweise können Sie eine vorkonfigurierte hochladen:

- Skript-Editor-Webpart, das JavaScript-Dateien auf der Remotewebsite verwendet.
    
- Inhaltssuche-Webpart.
    
In diesem Artikel wird das vor dem konfigurieren den Skript-Editor-Webpart JavaScript-Dateien auf der Remotewebsite verwenden, um Anpassung der Benutzeroberfläche auszuführen. Mit dieser Lösung können:

- Verwenden Sie die Skriptdateien aus dem remote Web in Webparts und nicht verweisenden Skripts aus der Liste **Websiteobjekte** auf dem hostweb.
    
- Bereitstellen von vorkonfigurierten Webparts in Ihrer benutzerdefinierten Site Bereitstellungsprozesses. Möglicherweise möchten Sie beispielsweise als Teil Ihrer benutzerdefinierten Site Bereitstellungsprozesses, Website Nutzungsinformationen Richtlinie für den Benutzer angezeigt wird, wenn eine neue Website erstellt wird. 
    
- Geladen Sie gefilterte Inhalte in Webparts für Ihre Benutzer automatisch. Beispielsweise kann Skriptdatei Lesen von einem externen System lokale Nachrichten Informationen anzeigen.
    
- Ermöglicht es Benutzern ihrer Website mithilfe von Webparts aus dem **Webpartkatalog**zusätzliche Funktionen hinzu.

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Laden Sie Sie zuerst [Core.AppScriptPart](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.AppScriptPart) -Beispiel-add-in des Projekts [Office365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="using-the-coreappscriptpart-add-in"></a>Mithilfe des Core.AppScriptPart-add-Ins

Wenn Sie das Codebeispiel ausführen und **Szenario ausführen**wählen:

1. Wählen Sie **zurück zur Website**.
    
2. **Seite**zum Auswählen von > **Bearbeiten** > **Einfügen** > **-Webpart**.
    
3. Wählen Sie in **Kategorien**die **Add-in-Skript Teil**, und dann **von Benutzerprofilinformationen**.
    
4. Klicken Sie auf **Hinzufügen**.
    
5. Wählen Sie in der Dropdown-Liste in der oberen rechten Ecke des Webparts **von Benutzerprofilinformationen** **Webpart bearbeiten**.
    
6. Wählen Sie **AUSSCHNITT bearbeiten**.
    
7. Überprüfen der ** &lt;Skript&gt; ** Element.
    
    Beachten Sie, dass das **Src** -Attribut Links zu einer JavaScript-auf die Remotewebsite Datei. Die ** &lt;Skript&gt; ** Element wird von der **Content** -Eigenschaft in der Core.AppScriptPartWeb\userprofileinformation.webpart festgelegt, wie im folgenden Beispiel dargestellt. Die JavaScript-Datei mit verknüpften durch das **Src** -Attribut ist Core.AppScriptPartWeb\Scripts\userprofileinformation.js. Userprofileinformation.js liest Profilinformationen des aktuellen Benutzers aus der Benutzerprofildienst und dann diese Informationen im Webpart angezeigt.
    
     **Hinweis:** Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

  ```XML
  <property name="Content" type="string">&amp;lt;script type="text/javascript" src="https://localhost:44361/scripts/userprofileinformation.js"&amp;gt;&amp;lt;/script&amp;gt;
&amp;lt;div id="UserProfileAboutMe"&amp;gt;&amp;lt;div&amp;gt;
  </property>
  ```

8. Wählen Sie **Abbrechen**.
    
9. Wählen Sie **Speichern** aus.

**Hinweis:** Wenn Ihre Benutzerprofil Bild nicht angezeigt wird, öffnen Sie Ihrer OneDrive for Business-Website, und klicken Sie dann mit der Hostwebsite zurückzugeben.

In Core.AppScriptPartWeb\Pages\Default.aspx führt **Szenario ausführen** **BtnScenario_Click**, die Folgendes ermöglicht:

1. Ruft einen Verweis auf den Ordner **Webpartkatalog** .
    
2. Wird verwendet, [komplexer FileCreationInformation](https://msdn.microsoft.com/library/office/microsoft.sharepoint.client.filecreationinformation.aspx) zum Erstellen der Datei userprofileinformation.webpart so vom Anbieter gehostete-add-in in den **Webpartkatalog**hoch. Der Ordner **. Files.Add** -Methode fügt die Datei dem **Webpartkatalog**hinzu.
    
3. Ruft alle Listenelemente in der **Webpart-Katalog**, und klicken Sie dann userprofileinformation.webpart gesucht.
    
4. Wenn userprofileinformation.webpart gefunden wird, weist das Webpart zu einer benutzerdefinierten Gruppe mit dem Namen **Add-in-Skript Teil**.

```C#
protected void btnScenario_Click(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var clientContext = spContext.CreateUserClientContextForSPHost())
            {
                var folder = clientContext.Web.Lists.GetByTitle("Web Part Gallery").RootFolder;
                clientContext.Load(folder);
                clientContext.ExecuteQuery();

                // Upload the "userprofileinformation.webpart" file.
                using (var stream = System.IO.File.OpenRead(
                                Server.MapPath("~/userprofileinformation.webpart")))
                {
                    FileCreationInformation fileInfo = new FileCreationInformation();
                    fileInfo.ContentStream = stream;
                    fileInfo.Overwrite = true;
                    fileInfo.Url = "userprofileinformation.webpart";
                    File file = folder.Files.Add(fileInfo);
                    clientContext.ExecuteQuery();
                }

                // Update the group that the Web Part belongs to. Start by getting all list items in the Web Part Gallery, and then find the Web Part that was just uploaded.
                var list = clientContext.Web.Lists.GetByTitle("Web Part Gallery");
                CamlQuery camlQuery = CamlQuery.CreateAllItemsQuery(100);
                Microsoft.SharePoint.Client.ListItemCollection items = list.GetItems(camlQuery);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
                foreach (var item in items)
                {
                    // Create new group.
                    if (item["FileLeafRef"].ToString().ToLowerInvariant() == "userprofileinformation.webpart")
                    {
                        item["Group"] = "add-in Script Part";
                        item.Update();
                        clientContext.ExecuteQuery();
                    }
                }

                lblStatus.Text = string.Format("add-in script part has been added to Web Part Gallery. You can find 'User Profile Information' script part under 'App Script Part' group in the <a href='{0}'>host web</a>.", spContext.SPHostUrl.ToString());
            }
        }
```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
    
- [Anpassen der Benutzeroberfläche der SharePoint-Benutzeroberfläche mithilfe von JavaScript](Customize-your-SharePoint-site-UI-by-using-JavaScript.md)
