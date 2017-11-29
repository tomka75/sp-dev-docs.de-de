---
title: Cross-Domain-Bildern in SharePoint gehostet durch Drittanbieter-add-ins
ms.date: 11/03/2017
ms.openlocfilehash: 3260b534a87fbb097fdaa5910a1c41f276514733
ms.sourcegitcommit: 65e885f547ca9055617fe0871a13c7fc85086032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2017
---
# <a name="cross-domain-images-in-sharepoint-provider-hosted-add-ins"></a><span data-ttu-id="9e634-102">Cross-Domain-Bildern in SharePoint gehostet durch Drittanbieter-add-ins</span><span class="sxs-lookup"><span data-stu-id="9e634-102">Cross-domain images in SharePoint provider-hosted add-ins</span></span>

<span data-ttu-id="9e634-103">Verwenden Sie Bilder in Domänen vom Anbieter gehosteten-add-ins.</span><span class="sxs-lookup"><span data-stu-id="9e634-103">Use images across domains in provider-hosted add-ins.</span></span>

<span data-ttu-id="9e634-104">_**Gilt für:** SharePoint 2013 | SharePoint-Add-ins | SharePoint Online_</span><span class="sxs-lookup"><span data-stu-id="9e634-104">_**Applies to:** SharePoint 2013 | SharePoint Add-ins | SharePoint Online_</span></span>

<span data-ttu-id="9e634-105">Möglicherweise möchten Bilder aus einer SharePoint-Website in der vom Anbieter gehosteten-add-ins anzuzeigen. Da vom Anbieter gehosteten-add-ins auf einer Remotewebsite ausgeführt werden, unterscheiden sich die Domänen für Ihr Add-in vom Anbieter gehostet und Ihrer SharePoint-Website.</span><span class="sxs-lookup"><span data-stu-id="9e634-105">You might want to display images from a SharePoint site in your provider-hosted add-ins. Because provider-hosted add-ins run on a remote web, the domains for your provider-hosted add-in and your SharePoint site are different.</span></span> <span data-ttu-id="9e634-106">Angenommen, Ihr Add-in möglicherweise in Windows Azure ausgeführt, und Sie versuchen, ein Bild aus Office 365 anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="9e634-106">For example, your add-in might run on Microsoft Azure, and you're trying to show an image from Office 365.</span></span> <span data-ttu-id="9e634-107">Da Ihr Add-in vom Anbieter gehosteten Domänen Zugriff auf das Bild überschreitet, erfordert SharePoint benutzerautorisierung, bevor das Add-in vom Anbieter gehosteten die Abbildung zeigt.</span><span class="sxs-lookup"><span data-stu-id="9e634-107">Because your provider-hosted add-in crosses domains to access the image, SharePoint requires user authorization before the provider-hosted add-in shows the image.</span></span>

<span data-ttu-id="9e634-108">Das [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) -Codebeispiel wird veranschaulicht, wie ein vom Anbieter gehosteten add-in einer SharePoint-Zugriffstoken und REST-Dienst zum Abrufen von Bildern aus SharePoint verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="9e634-108">The [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) code sample shows how a provider-hosted add-in can use a SharePoint access token and a REST service to retrieve images from SharePoint.</span></span> <span data-ttu-id="9e634-109">Der REST-Dienst gibt eine Base64-codierte Zeichenfolge, die verwendet wird, um das Bild im Browser anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="9e634-109">The REST service returns a Base64-encoded string, which is used to show the image in the browser.</span></span> <span data-ttu-id="9e634-110">Verwenden Sie die Lösung in diesem Beispiel zum Anzeigen von Bildern in vom Anbieter gehosteten-add-ins mithilfe von serverseitigen oder mithilfe der clientseitigen Code in SharePoint gespeichert.</span><span class="sxs-lookup"><span data-stu-id="9e634-110">Use the solution in this sample to show images stored in SharePoint in provider-hosted add-ins by using either server-side or client-side code.</span></span>

<span data-ttu-id="9e634-111">**Hinweis:** Da das Beispiel einen REST-Endpunkt verwendet wird, können Sie serverseitigen oder mithilfe der clientseitigen Code verwenden, um Ihr Bild abzurufen.</span><span class="sxs-lookup"><span data-stu-id="9e634-111">**Note:** Because the sample uses a REST endpoint, you can use either server-side or client-side code to retrieve your image.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9e634-112">Bevor Sie beginnen:</span><span class="sxs-lookup"><span data-stu-id="9e634-112">Before you begin</span></span>

<span data-ttu-id="9e634-113">Laden Sie Sie zuerst [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) -Beispiel-add-in des Projekts [Office 365 Developer Mustern und Methoden](https://github.com/SharePoint/PnP/tree/dev) von GitHub.</span><span class="sxs-lookup"><span data-stu-id="9e634-113">To get started, download the [Core.CrossDomainImages](https://github.com/SharePoint/PnP/tree/dev/Samples/Core.CrossDomainImages) sample add-in from the [Office 365 Developer patterns and practices](https://github.com/SharePoint/PnP/tree/dev) project on GitHub.</span></span>

## <a name="using-the-corecrossdomainimages-code-sample"></a><span data-ttu-id="9e634-114">Mithilfe des Codebeispiels Core.CrossDomainImages</span><span class="sxs-lookup"><span data-stu-id="9e634-114">Using the Core.CrossDomainImages code sample</span></span>

<span data-ttu-id="9e634-115">Wenn Sie dieses Beispiel ausführen, versucht Default.aspx folgenden geladen werden:</span><span class="sxs-lookup"><span data-stu-id="9e634-115">When you run this sample, Default.aspx tries to load the following:</span></span>

- <span data-ttu-id="9e634-116">Bild 1, über die absolute URL.</span><span class="sxs-lookup"><span data-stu-id="9e634-116">Image 1, by using the absolute URL.</span></span> 
    
- <span data-ttu-id="9e634-117">Abbildung 2, mit einem serverseitigen Aufruf an einen REST-Endpunkt, der eine Base64-codierte Zeichenfolge zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="9e634-117">Image 2, by using a server-side call to a REST endpoint that returns a Base64-encoded string.</span></span>
    
- <span data-ttu-id="9e634-118">Bild 3, mit einem Aufruf mithilfe der clientseitigen an einen REST-Endpunkt, der eine Base64-codierte Zeichenfolge zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="9e634-118">Image 3, by using a client-side call to a REST endpoint that returns a Base64-encoded string.</span></span>
    
<span data-ttu-id="9e634-119">**Hinweis:** Abbildung 1 wird, da das Add-in Domänen, um das Bild in SharePoint abzurufen schneidet nicht gerendert.</span><span class="sxs-lookup"><span data-stu-id="9e634-119">**Note:** Image 1 does not render because the add-in crosses domains to get to the image in SharePoint.</span></span> <span data-ttu-id="9e634-120">Beachten Sie, dass die URL des vom Anbieter gehosteten-add-Ins auf Localhost ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="9e634-120">Notice that the URL of the provider-hosted add-in runs on localhost.</span></span> <span data-ttu-id="9e634-121">Öffnen Sie das Kontextmenü (Rechtsklick) für Bild 1 ein, und wählen Sie dann auf **Eigenschaften**.</span><span class="sxs-lookup"><span data-stu-id="9e634-121">Open the shortcut menu (right-click) for Image 1, and then choose **Properties**.</span></span> <span data-ttu-id="9e634-122">Beachten Sie, dass die **Adresse (URL)** das Bild aus dem Web-Add-in, nicht Localhost abrufen möchte.</span><span class="sxs-lookup"><span data-stu-id="9e634-122">Notice that the **Address (URL)** is trying to retrieve the image from the add-in web, not localhost.</span></span> <span data-ttu-id="9e634-123">Da das vom Anbieter gehosteten-Add-in Domänen, die zum Erreichen der Add-ins Web überschreitet, ist die Authentifizierung erforderlich, um das Bild zugreifen.</span><span class="sxs-lookup"><span data-stu-id="9e634-123">Because the provider-hosted add-in crosses domains to reach the add-in web, authentication is required in order to access the image.</span></span> <span data-ttu-id="9e634-124">Stellen Sie sicher, dass den Zugriff auf Bild 1 URL direkt, im Gegensatz zu den domänenübergreifenden Anruf in der vom Anbieter gehosteten-add-in, ohne Fehler aufgelöst wird durch Kopieren und Einfügen des **Felds Webadresse (URL)** in einem neuen Browserfenster geöffnet.</span><span class="sxs-lookup"><span data-stu-id="9e634-124">Verify that accessing Image 1's URL directly, as opposed to the cross-domain call in the provider-hosted add-in, resolves without an error by copying and pasting **Address (URL)** into a new browser window.</span></span> <span data-ttu-id="9e634-125">Beachten Sie, dass Bild 1 ohne Fehler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="9e634-125">Notice that Image 1 displays without an error.</span></span> <span data-ttu-id="9e634-126">Vergleichen Sie die Quelle der Bild 1 auf die Quelle des Bilds 2.</span><span class="sxs-lookup"><span data-stu-id="9e634-126">Compare the source of Image 1 to the source of Image 2.</span></span> <span data-ttu-id="9e634-127">Beachten Sie, dass die **Adresse (URL)** in eine Base64-codierte Zeichenfolge zeigt.</span><span class="sxs-lookup"><span data-stu-id="9e634-127">Notice that the **Address (URL)** points to a Base64-encoded string.</span></span>

<span data-ttu-id="9e634-128">Beim Laden von Default.aspx **Page_Load** wird ausgeführt und führt folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="9e634-128">When Default.aspx loads, **Page_Load** runs and does the following:</span></span>

1. <span data-ttu-id="9e634-129">Image1.ImageUrl festgelegt auf den absoluten Pfad des Bilds.</span><span class="sxs-lookup"><span data-stu-id="9e634-129">Sets Image1.ImageUrl to the absolute path of the image.</span></span>
    
2. <span data-ttu-id="9e634-130">ImgService instanziiert.</span><span class="sxs-lookup"><span data-stu-id="9e634-130">Instantiates ImgService.</span></span> <span data-ttu-id="9e634-131">ImgService ist eine REST-Endpunkt, der in derselben Domäne wie das vom Anbieter gehosteten-add-in ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="9e634-131">ImgService is a REST endpoint that runs in the same domain as the provider-hosted add-in.</span></span>
    
3. <span data-ttu-id="9e634-132">Legt Image2.ImageUrl auf die Base64-codierte Zeichenfolge, die **ImgService.GetImage** zurückgibt.</span><span class="sxs-lookup"><span data-stu-id="9e634-132">Sets Image2.ImageUrl to the Base64-encoded string that **ImgService.GetImage** returns.</span></span> <span data-ttu-id="9e634-133">Zugriffstoken, Website, Ordner und Dateinamen werden **ImgService.GetImage**als Parameter übergeben.</span><span class="sxs-lookup"><span data-stu-id="9e634-133">Access token, site, folder, and file name are passed as parameters to **ImgService.GetImage**.</span></span>
    
<span data-ttu-id="9e634-134">**Hinweis:** Der Code in diesem Artikel wird als bereitgestellt-ist, ohne Garantie jeglicher Art, sei Sie ausdrücklich oder konkludent, einschließlich konkludente Garantien der Eignung für einen bestimmten Zweck, Makro- oder nichtverletzung.</span><span class="sxs-lookup"><span data-stu-id="9e634-134">**Note:** The code in this article is provided as-is, without warranty of any kind, either express or implied, including any implied warranties of fitness for a particular purpose, merchantability, or non-infringement.</span></span>

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

<span data-ttu-id="9e634-135">**GetImage** bewirkt Folgendes:</span><span class="sxs-lookup"><span data-stu-id="9e634-135">**GetImage** does the following:</span></span>

1. <span data-ttu-id="9e634-136">Verwendet **Url** zum Speichern des GetFolderByServerRelativeUrl-REST-Endpunkts-URI, der verwendet wird, um das Bild aus SharePoint abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="9e634-136">Uses **url** to store the GetFolderByServerRelativeUrl REST endpoint URI, which will be used to retrieve the image from SharePoint.</span></span> <span data-ttu-id="9e634-137">Erfahren Sie unter [verweisen auf Dateien und Ordner-REST-API](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e634-137">You can learn more at [Files and folders REST API reference](http://msdn.microsoft.com/library/2c3d2545-1cd7-497e-b535-12199d8edfbb%28Office.15%29.aspx).</span></span>
    
2. <span data-ttu-id="9e634-138">Instanziiert ein [HttpWebRequest](https://msdn.microsoft.com/library/system.net.httpwebrequest.aspx) -Objekt mit der **Url** .</span><span class="sxs-lookup"><span data-stu-id="9e634-138">Instantiates an [HttpWebRequest](https://msdn.microsoft.com/library/system.net.httpwebrequest.aspx) object by using **url** .</span></span>
    
3. <span data-ttu-id="9e634-139">Das HttpWebRequest-Objekt, das Zugriffstoken enthält, hinzugefügt eine Authorization-Kopfzeile.</span><span class="sxs-lookup"><span data-stu-id="9e634-139">Adds an Authorization header to the HttpWebRequest object that contains the access token.</span></span> 
    
<span data-ttu-id="9e634-140">Nachdem der GET-Aufruf an den Endpunkt-URI erfolgt, ist der zurückgegebene Stream eine Base64-codierte Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="9e634-140">After the GET call is made to the endpoint URI, the returned stream is a Base64-encoded string.</span></span> <span data-ttu-id="9e634-141">Die zurückgegebene Zeichenfolge wird auf das **Src** -Attribut des Bilds festgelegt.</span><span class="sxs-lookup"><span data-stu-id="9e634-141">The returned string is set to the **src** attribute of the image.</span></span>

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

<span data-ttu-id="9e634-142">Nach Abschluss der **Page_Load** führt Default.aspx den clientseitigen Code default.aspx das Bild 3 lädt.</span><span class="sxs-lookup"><span data-stu-id="9e634-142">After **Page_Load** finishes, Default.aspx runs the client-side code in Default.aspx, which loads Image 3.</span></span> <span data-ttu-id="9e634-143">Der mithilfe der clientseitigen Code ruft **GetImage** mithilfe von jQuery Ajax.</span><span class="sxs-lookup"><span data-stu-id="9e634-143">The client-side code calls **GetImage** by using jQuery Ajax.</span></span> <span data-ttu-id="9e634-144">Wenn **GetImage** erfolgreich die Base64-codierte Zeichenfolge zurückgegeben wird, wird das **Src** -Attribut Image3 auf die zurückgegebene Zeichenfolge festgelegt.</span><span class="sxs-lookup"><span data-stu-id="9e634-144">When **GetImage** returns the Base64-encoded string successfully, the **src** attribute on Image3 is set to the returned string.</span></span>

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

## <a name="additional-resources"></a><span data-ttu-id="9e634-145">Zusätzliche Ressourcen</span><span class="sxs-lookup"><span data-stu-id="9e634-145">Additional resources</span></span>
<span data-ttu-id="9e634-146"><a name="bk_addresources"> </a></span><span class="sxs-lookup"><span data-stu-id="9e634-146"></span></span>

- [<span data-ttu-id="9e634-147">Lösungsleitfaden für Office 365-Entwicklungsmuster und -Vorgehensweisen</span><span class="sxs-lookup"><span data-stu-id="9e634-147">Office 365 development patterns and practices solution guidance</span></span>](Office-365-development-patterns-and-practices-solution-guidance.md)
