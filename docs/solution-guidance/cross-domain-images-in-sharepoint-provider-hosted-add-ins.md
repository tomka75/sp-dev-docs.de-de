---
title: Cross-Domain-Bildern in SharePoint gehostet durch Drittanbieter-add-ins
ms.date: 11/03/2017
ms.openlocfilehash: 3260b534a87fbb097fdaa5910a1c41f276514733
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="cross-domain-images-in-sharepoint-provider-hosted-add-ins"></a>Cross-Domain-Bildern in SharePoint gehostet durch Drittanbieter-add-ins

Verwenden Sie Bilder in Domänen vom Anbieter gehosteten-add-ins.

_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_

Möglicherweise möchten Bilder aus einer SharePoint-Website in der vom Anbieter gehosteten-add-ins anzuzeigen. Da vom Anbieter gehosteten-add-ins auf einer Remotewebsite ausgeführt werden, unterscheiden sich die Domänen für Ihr Add-in vom Anbieter gehostet und Ihrer SharePoint-Website. Angenommen, Ihr Add-in möglicherweise in Windows Azure ausgeführt, und Sie versuchen, ein Bild aus Office 365 anzuzeigen. Da Ihr Add-in vom Anbieter gehosteten Domänen Zugriff auf das Bild überschreitet, erfordert SharePoint benutzerautorisierung, bevor das Add-in vom Anbieter gehosteten die Abbildung zeigt.

Das [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) -Codebeispiel wird veranschaulicht, wie ein vom Anbieter gehosteten add-in einer SharePoint-Zugriffstoken und REST-Dienst zum Abrufen von Bildern aus SharePoint verwenden kann. Der REST-Dienst gibt eine Base64-codierte Zeichenfolge, die verwendet wird, um das Bild im Browser anzuzeigen. Verwenden Sie die Lösung in diesem Beispiel zum Anzeigen von Bildern in vom Anbieter gehosteten-add-ins mithilfe von serverseitigen oder mithilfe der clientseitigen Code in SharePoint gespeichert.

**Hinweis:** Da das Beispiel einen REST-Endpunkt verwendet wird, können Sie serverseitigen oder mithilfe der clientseitigen Code verwenden, um Ihr Bild abzurufen.

## <a name="before-you-begin"></a>Bevor Sie beginnen:

Laden Sie Sie zuerst [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.

## <a name="using-the-corecrossdomainimages-code-sample"></a>Mithilfe des Codebeispiels Core.CrossDomainImages

Wenn Sie dieses Beispiel ausführen, versucht Default.aspx folgenden geladen werden:

- Bild 1, über die absolute URL. 
    
- Abbildung 2, mit einem serverseitigen Aufruf an einen REST-Endpunkt, der eine Base64-codierte Zeichenfolge zurückgibt.
    
- Bild 3, mit einem Aufruf mithilfe der clientseitigen an einen REST-Endpunkt, der eine Base64-codierte Zeichenfolge zurückgibt.
    
**Hinweis:** Abbildung 1 wird, da das Add-in Domänen, um das Bild in SharePoint abzurufen schneidet nicht gerendert. Beachten Sie, dass die URL des vom Anbieter gehosteten-add-Ins auf Localhost ausgeführt wird. Öffnen Sie das Kontextmenü (Rechtsklick) für Bild 1 ein, und wählen Sie dann auf **Eigenschaften**. Beachten Sie, dass die **Adresse (URL)** das Bild aus dem Web-Add-in, nicht Localhost abrufen möchte. Da das vom Anbieter gehosteten-Add-in Domänen, die zum Erreichen der Add-ins Web überschreitet, ist die Authentifizierung erforderlich, um das Bild zugreifen. Stellen Sie sicher, dass den Zugriff auf Bild 1 URL direkt, im Gegensatz zu den domänenübergreifenden Anruf in der vom Anbieter gehosteten-add-in, ohne Fehler aufgelöst wird durch Kopieren und Einfügen des **Felds Webadresse (URL)** in einem neuen Browserfenster geöffnet. Beachten Sie, dass Bild 1 ohne Fehler angezeigt. Vergleichen Sie die Quelle der Bild 1 auf die Quelle des Bilds 2. Beachten Sie, dass die **Adresse (URL)** in eine Base64-codierte Zeichenfolge zeigt.

Beim Laden von Default.aspx **Page_Load** wird ausgeführt und führt folgende Schritte aus:

1. Image1.ImageUrl festgelegt auf den absoluten Pfad des Bilds.
    
2. ImgService instanziiert. ImgService ist eine REST-Endpunkt, der in derselben Domäne wie das vom Anbieter gehosteten-add-in ausgeführt wird.
    
3. Legt Image2.ImageUrl auf die Base64-codierte Zeichenfolge, die **ImgService.GetImage** zurückgibt. Zugriffstoken, Website, Ordner und Dateinamen werden **ImgService.GetImage**als Parameter übergeben.
    
**Hinweis:** Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.

```C#
 protected void Page_Load(object sender, EventArgs e)
        {
            var spContext = SharePointContextProvider.Current.GetSharePointContext(Context);
            using (var clientContext = spContext.CreateUserClientContextForSPAppWeb())
            {
                // Set the access token in a hidden field for client-side code to use.
                hdnAccessToken.Value = spContext.UserAccessTokenForSPAppWeb;

                // Set the URLs to the images.
                Image1.ImageUrl = spContext.SPAppWebUrl + "AppImages/O365.png";
                Services.ImgService svc = new Services.ImgService();
                Image2.ImageUrl = svc.GetImage(spContext.UserAccessTokenForSPAppWeb, spContext.SPAppWebUrl.ToString(), "AppImages", "O365.png");
            }
        }
```

**GetImage** bewirkt Folgendes:

1. Verwendet **Url** zum Speichern des GetFolderByServerRelativeUrl-REST-Endpunkts-URI, der verwendet wird, um das Bild aus SharePoint abgerufen werden. Erfahren Sie unter [verweisen auf Dateien und Ordner-REST-API](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx).
    
2. Instanziiert ein [HttpWebRequest](https://msdn.microsoft.com/library/system.net.httpwebrequest.aspx) -Objekt mit der **Url** .
    
3. Das HttpWebRequest-Objekt, das Zugriffstoken enthält, hinzugefügt eine Authorization-Kopfzeile. 
    
Nachdem der GET-Aufruf an den Endpunkt-URI erfolgt, ist der zurückgegebene Stream eine Base64-codierte Zeichenfolge. Die zurückgegebene Zeichenfolge wird auf das **Src** -Attribut des Bilds festgelegt.

```C#
 public string GetImage(string accessToken, string site, string folder, string file)
        {
            // Create the HttpWebRequest to call the REST endpoint.
            string url = String.Format("{0}_api/web/GetFolderByServerRelativeUrl('{1}')/Files('{2}')/$value", site, folder, file);
            HttpWebRequest request = WebRequest.Create(url) as HttpWebRequest;
            request.Headers.Add("Authorization", "Bearer" + " " + accessToken);
            using (HttpWebResponse response = request.GetResponse() as HttpWebResponse)
            {
                using (var sourceStream = response.GetResponseStream())
                {
                    using (var newStream = new MemoryStream())
                    {
                        sourceSteam.CopyTo(newStream);
                        byte[] bytes = newStream.ToArray();
                        return "data:image/png;base64, " + Convert.ToBase64String(bytes);
                    }
                }
            }
        }
```

Nach Abschluss der **Page_Load** führt Default.aspx den clientseitigen Code default.aspx das Bild 3 lädt. Der mithilfe der clientseitigen Code ruft **GetImage** mithilfe von jQuery Ajax. Wenn **GetImage** erfolgreich die Base64-codierte Zeichenfolge zurückgegeben wird, wird das **Src** -Attribut Image3 auf die zurückgegebene Zeichenfolge festgelegt.

```
  ...

                  $.ajax({
                url: '../Services/ImgService.svc/GetImage?accessToken=' + $('#hdnAccessToken').val() + '&amp;site=' + encodeURIComponent(appWebUrl + '/') + '&amp;folder=AppImages&amp;file=O365.png',
                dataType: 'json',
                success: function (data) {
                    $('#Image3').attr('src', data.d);
                },
                error: function (err) {
                    alert('error occurred');
                }
            });

           ...

```

## <a name="additional-resources"></a>Zusätzliche Ressourcen
<a name="bk_addresources"> </a>

- [Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen](Office-365-development-patterns-and-practices-solution-guidance.md)
